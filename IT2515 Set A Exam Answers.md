# IT2515 Practical Test Set A — Answers (Hidden by Default)

## Question 1 — Array Management, Iteration and Advanced Logic (7 marks)

### (i) Create an array with three service names

```powershell
$services = @('WinDefend', 'vds', 'Spooler')
```

### (ii) ForEach loop to check service status

```powershell
foreach ($service in $services) {
    $status = (Get-Service -Name $service).Status
    # ... if-elseif-else block here
}
```

### (iii) Complete Question 1 Solution

```powershell
$services = @('WinDefend', 'vds', 'Spooler')

foreach ($service in $services) {
    $svc = Get-Service -Name $service -ErrorAction SilentlyContinue
    if ($svc -eq $null) {
        Write-Host "$service : Not Found" -ForegroundColor Red
    }
    elseif ($svc.Status -eq 'Running') {
        Write-Host "$service : Running" -ForegroundColor Green
    }
    elseif ($svc.Status -eq 'Stopped') {
        Write-Host "$service : Stopped" -ForegroundColor Yellow
    }
    else {
        Write-Host "$service : $($svc.Status)" -ForegroundColor Red
    }
}
```

**Key Points:**
- Array created with `@()` syntax
- `ForEach` iterates through each service name
- `Get-Service -Name $service` retrieves the service object
- `-ErrorAction SilentlyContinue` handles missing services gracefully
- `Write-Host -ForegroundColor` sets the console color
- `Green` for Running, `Yellow` for Stopped, `Red` for anything else (including missing)

---

## Question 2 — Command Mastery and Output Redirection (3 marks)

### Complete Question 2 Solution

```powershell
Get-Process | Sort-Object -Property ID > Audit_Report.txt
echo "Audit Complete - $(Get-Date)" >> Audit_Report.txt
```

**Or broken down:**

```powershell
# (i) Retrieve all running processes and (ii) sort by ID (lowest to highest)
Get-Process | Sort-Object -Property ID > Audit_Report.txt

# (iv) Append timestamped "Audit Complete" message
echo "Audit Complete - $(Get-Date)" >> Audit_Report.txt
```

**Key Points:**
- `Get-Process` retrieves all running processes
- `Sort-Object -Property ID` sorts by Process Identifier (default is ascending = lowest to highest)
- `>` redirects output to file (overwrites if exists)
- `>>` appends to file (doesn't overwrite)
- `$(Get-Date)` inserts the current timestamp
- `echo` is an alias for `Write-Output`

---

## Complete CheckSecurity.ps1 Script

```powershell
# Question 1 - Service Status Check
$services = @('WinDefend', 'vds', 'Spooler')

foreach ($service in $services) {
    $svc = Get-Service -Name $service -ErrorAction SilentlyContinue
    if ($svc -eq $null) {
        Write-Host "$service : Not Found" -ForegroundColor Red
    }
    elseif ($svc.Status -eq 'Running') {
        Write-Host "$service : Running" -ForegroundColor Green
    }
    elseif ($svc.Status -eq 'Stopped') {
        Write-Host "$service : Stopped" -ForegroundColor Yellow
    }
    else {
        Write-Host "$service : $($svc.Status)" -ForegroundColor Red
    }
}

# Question 2 - Process Audit Report
Get-Process | Sort-Object -Property ID > Audit_Report.txt
echo "Audit Complete - $(Get-Date)" >> Audit_Report.txt
```

---

## Marking Breakdown (What the Professor Looks For)

### Question 1 (7 marks):
| Item | Marks | What's Tested |
|------|-------|---------------|
| Correct array creation with 3 services | 1 | Array syntax `@()` |
| ForEach loop structure | 1 | Correct loop syntax |
| Get-Service usage inside loop | 1 | Cmdlet knowledge |
| If block for Running (Green) | 1 | Conditional + color |
| ElseIf block for Stopped (Yellow) | 1 | Conditional + color |
| Else block for other/missing (Red) | 1 | Error handling |
| Overall script logic flow | 1 | Integration |

### Question 2 (3 marks):
| Item | Marks | What's Tested |
|------|-------|---------------|
| Get-Process piped to Sort-Object by ID | 1 | Pipeline + Sort |
| Save to Audit_Report.txt using > | 1 | Redirection operator |
| Echo timestamped message using >> | 1 | Append + Get-Date |

---

## Revision Paper Answers (For Practice)

### Q1. Redirection Operators (4 marks)
**> operator:** Overwrites the target file. If the file already contains data, all existing data is **replaced** with the new output.

**>> operator:** Appends to the target file. If the file already contains data, the new output is **added after** the existing data.

### Q2. The Pipeline (3 marks)
When data is passed through the pipeline operator `|`, the **output object** of the first command is passed as **input** to the second command. PowerShell passes **objects** (not text streams like traditional shells).

Example: `Get-Process | Sort-Object` — Get-Process outputs process objects, which are piped to Sort-Object. Sort-Object receives these objects and sorts them by their properties.

### Q3. Conditional Operators (4 marks)
| Meaning | PowerShell Operator |
|---------|-------------------|
| Equals to | `-eq` |
| Not equal to | `-ne` |
| Greater than | `-gt` |
| Less than or equal to | `-le` |

### Q4. Error Handling (4 marks)
The parameter is **`-ErrorAction SilentlyContinue`**. When added to `Get-Service`, it suppresses the error that would occur when querying a non-existent service. This allows the script to continue running and lets an If-Else block check if the returned value is `$null` to gracefully handle missing services.

### Q5. Array and Foreach Script (4 marks)
```powershell
$numbers = @(1, 3, 5, 7, 9)
foreach ($num in $numbers) {
    echo $num
}
```
