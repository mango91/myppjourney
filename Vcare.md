How I created the Pflege Score

1) Create a collection colScoring with dummy variables
   in Application > OnStart
2) Calculation on Screen scrForm - New Calc
   
   Form Form-Rating
   Rating_DataCard4 >> DataCardValue10 ist für "normale Bewertung"
   *Default Property*: bedeutet wenn die Collection nicht leer, dann finde die Zeile ansonsten 0

        Funktion:
                   If(!IsBlank
                   (LookUp(colScoring, Question = 'Gallery-Question'.Selected.'Question-ID' && Client =
                   galAssessments_2.Selected.Name)),
                   LookUp(colScoring, Question = 'Gallery-Question'.Selected.'Question-ID' && Client =
                   galAssessments_2.Selected.Name, Score),  0)

   *OnChange Property*:

   Nutze die Patch funktion, bedeutet - finde das Modul mit der Frage und speichere das Rating (Self.Value) als Score
   ab. Falls eine Gewichtung vorhanden ist, speichere den gewichteten Wert in ScaleScore ab.
   Die Gewichtung (Scale) ist in der Dataverse Table Questions abgespeichert (e.g. Question-ID "Ich kann alleine
   Essen und Trinken" hat einen Scale von 2,50)

   Erstelle eine neue Collection "colModulScore" und erstelle die Summe von ScaleScore pro Modul (abgerundet).

   Funktion:
   
                   Patch(colScoring, {Modul: 'Gallery-Modul'.Selected.Name, Question: 'Gallery
                   Question'.Selected.'Question-ID', Client: galAssessments_2.Selected.Name}, {Modul: 'Gallery
                   Modul'.Selected.Name, Question: 'Gallery-Question'.Selected.'Question-ID', Client:
                   galAssessments_2.Selected.Name, Score: Self.Value, ScaleScore: If(LookUp(colScoring, Client =
                   galAssessments_2.Selected.Name && Modul = 'Gallery-Modul'.Selected.Name && Question = 'Gallery
                   Question'.Selected.'Question-ID',Score) = 0, 0,
                   Sum(Self.Value,'Gallery-Question'.Selected.Scale))});

                RemoveIf(colScoring, IsBlank(Question));
                ClearCollect(colModulScore, AddColumns(GroupBy(colScoring, "Client", "Modul", "GroupModul"), 
                "ModulScore", Round(Sum(GroupModul, ScaleScore),0)));

   *In der Gallery-TempScore* werden die Module gewichtet und das gewichtete Rating pro Modul errechnet.
   im Item WeightedRating - Text Property:

                   "Gewichtetes Rating: " & LookUp(Weights, ModulW = ThisItem.Modul && RoundedScore =
                   ThisItem.ModulScore, WeightedScore)

   in Item Modulscore_1 - Text Property wird Gewichtung abgespeichert:
   
           LookUp(Weights, ModulW = ThisItem.Modul && RoundedScore = ThisItem.ModulScore, WeightedScore) *                         LookUp(Modules, Name = ThisItem.Modul, Gewichtung)
   
   
   *in Form Form-Gesamtscore* wird in Datacard Gesamtscore_Datacard1 Default Property die Summe errechnet:
   Sum('Gallery-TempScore'.AllItems,Modulscore_1)
   Diese wird in der Datascource Clients abgespeichert. 
