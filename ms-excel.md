# Microsoft Excel tips

:leftwards_arrow_with_hook: Shortcut to type a line break:
- in a cell: `ALT`+`ENTER`
- in the _Find and Replace_ window: `CTRL`+`J`

&nbsp;

:arrows_counterclockwise: Shortcut to refresh cell values: `CTRL`+`ALT`+`F9`

&nbsp;

:no_entry_sign: Custom cell format definition to hide its content: `;;;`

&nbsp;

:scissors: Extract text from cell content using a regular expression in [VBA](https://en.wikipedia.org/wiki/Visual_Basic_for_Applications):
- In cell: ```=extractInfo(<cell>;<index>)```
- In VBA code:
```vba
Private Const ExtractPattern As String = "^Book\[author='(.*)', title='(.*)', year='([0-9]+)'\]$"

Private Function extractInfo(cell As range, index As Integer) As String
    Dim regex As New RegExp
    
    With regex
        .Global = True
        .MultiLine = True
        .IgnoreCase = False
        .pattern = ExtractPattern
    End With

    Set matches = regex.Execute(cell.Value)
    If matches.Count = 1 Then
        extractInfo = matches.Item(0).SubMatches.Item(index)
    End If
    Set matches = Nothing

End Function
```
- Example:
<table>
  <tr>
    <th></th>
    <th>A</th>
    <th>B</th>
    <th>C</th>
    <th>D</th>
  </tr>
  <tr>
    <th>1</th>
    <td>Book[author='A. Clément', title='Destinée', year='2011']</td>
    <td>A. Clément<br/><code>=extractInfo($A1;0)</code></td>
    <td>Destinée<br/><code>=extractInfo($A1;1)</code></td>
    <td>2011<br/><code>=extractInfo($A1;2)</code></td>
  </tr>
  <tr>
    <th>2</th>
    <td>Book[author='B. Bionti', title='Amore', year='1999']</td>
    <td>B. Pietri<br/><code>=extractInfo($A2;0)</code></td>
    <td>Amore<br/><code>=extractInfo($A2;1)</code></td>
    <td>1999<br/><code>=extractInfo($A2;2)</code></tr>
  <tr>
    <th>3</th>
    <td>Book[author='C. Clarks', title='Time', year='2014']</td>
    <td>C. Clarks<br/><code>=extractInfo($A3;0)</code></td>
    <td>Time<br/><code>=extractInfo($A3;1)</code></td>
    <td>2014<br/><code>=extractInfo($A3;2)</code></td>
  </tr>
</table>
