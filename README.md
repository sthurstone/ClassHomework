#VBA Scripting for Multi-year-stock-data
  #Through VBA Scripting for Excel we were able to calculate and output the annual percentage change, annual numerical/$ change as the total stock volume. 

Sub Mutlti_Year_Stock_Data()

'Declaring variables
    Dim Ticker As String
    Dim Yearly_Change As Long
    Dim Percent_Change As Long
    Dim Total_stock_volume As Double
    Dim Year_Open As Double
    Dim Year_Close As Double
    Dim i As Long
    
'Count and define number of worksheets within workbook and loop thru entire workbook to loop through

For Each ws In Worksheets
    
'Insert output headers and variables for calculations

    ws.Cells(1, 9).Value = "Ticker"
    ws.Cells(1, 10).Value = "Yearly Change"
    ws.Cells(1, 11).Value = "Percent Change"
    ws.Cells(1, 12).Value = "Total Stock Volume"
    ws.Cells(1, 15).Value = "Ticker"
    ws.Cells(1, 16).Value = "Value"
    ws.Cells(2, 14).Value = "Greatest % Increase"
    ws.Cells(3, 14).Value = "Greatest % Decrease"
    ws.Cells(4, 14).Value = "Greatest Total Volume"
    End_Row_Count = Range("A2", Range("A2").End(xlDown)).Rows.Count
          
                        
    'Determine output value for ticker
        
For i = 2 To End_Row_Count
    
    ws.Cells(i, 9).Value = ws.Cells(i, 1)

    'Determine output value for yearly_change

    ws.Cells(i, 10).Value = ws.Cells(i, 3) - ws.Cells(i, 6)
    If ws.Cells(i, 10).Value >= 0 Then
        ws.Cells(i, 10).Interior.ColorIndex = 4
    Else
        ws.Cells(i, 10).Interior.ColorIndex = 3
    End If
    
    'Determine output value for total_stock_volume
    
    ws.Cells(i, 12).Value = ws.Cells(i, 3) * ws.Cells(i, 7)

    'Determine output value for percent_change
    
    If ws.Cells(i, 11).Value >= 0 Then
        ws.Cells(i, 11).Interior.ColorIndex = 4
    Else
        ws.Cells(i, 11).Interior.ColorIndex = 3
    End If
    
    If ws.Cells(i, 6) = 0 Then
        ws.Cells(i, 11).Value = "NA"
Else
      ws.Cells(i, 11).Value = ws.Cells(i, 10) / ws.Cells(i, 6) * 100

End If

Next i

      Range("P2").Value = Application.Max(ws.Cells(i, 11))
      Range("P3").Value = Application.Min(ws.Cells(i, 11))
      Range("P4").Value = Application.MaxChange(ws.Cells(i, 12))
      
                
Next

End Sub
