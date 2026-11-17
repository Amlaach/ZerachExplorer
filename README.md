# ZerachExplorer | זרח אקספלורר

[![Build, Test & Release](https://github.com/Amlaach/ZerachExplorer/actions/workflows/ci.yml/badge.svg)](https://github.com/Amlaach/ZerachExplorer/actions/workflows/ci.yml)
![.NET 8](https://img.shields.io/badge/.NET-8.0%20LTS-512BD4)
![License](https://img.shields.io/badge/License-BSD--3--Clause-blue)

**זרח אקספלורר** (גרסה 1.7.0) הוא סייר קבצים מודרני, מאובטח וקל משקל ב-WPF (.NET 8), המיועד לעמדות מחשבים ציבוריות (בתי מדרש, ישיבות, ספריות, מוסדות ציבור וקיוסקים).

---

## 🧭 גלגולו של הפרויקט וקרדיטים (Project Lineage & Credits)

הפרויקט נבנה בשלושה שלבים היסטוריים המבוססים זה על גבי זה, תחת רישיון **BSD 3-Clause License**:

1. **הפרויקט המקורי — `LiteExplorer` מאת [`tempous`](https://github.com/tempous/LiteExplorer)**  
   הבסיס הטכנולוגי של התוכנה נוצר על ידי **tempous** בפרויקט הקוד הפתוח **LiteExplorer** — סייר קבצים קליל, מהיר ואסתטי ב-WPF וב-C#, הכולל תמיכה בכרטיסיות (Tabs), ממשק מודרני מבוסס WPF-UI, וניווט בסיסי במערכת הקבצים.
2. **הפיצול וההסבה לעמדות ציבוריות — `ZerachExplorer` (v1.4.0) מאת [`אביי (abaye123)`](https://github.com/abaye123/ZerachExplorer)**  
   **אביי** לקח את `tempous/LiteExplorer` והסב אותו ל**זרח אקספלורר** — סייר קבצים ייעודי ומאובטח לעמדות מחשב ציבוריות בבתי מדרש ובישיבות:
   * תרגום והתאמה מלאה לעברית ולכיווניות ימין-לשמאל (`RTL`).
   * חסימת גישה לכונן המערכת (`C:`) ולקבצים/תיקיות מוסתרים.
   * זיהוי וחסימה של כונני תוכנת **"אוצר החוכמה"**.
   * הגבלת פתיחה והעתקה לסיומות מסמכים מאושרות בלבד (`doc`, `docx`, `xls`, `xlsx`, `pdf`, `txt`, `csv`, `one`, `onetoc2`).
   * יצירת מיתוג, אייקון וחבילת התקנה לעמדות קצה.  
   *(אתר: [abaye.co](https://abaye.co) | תמיכה: `cs@abaye.co`)*
3. **ההרחבה, ההקשחה והמודרניזציה — גרסאות v1.5.0 – v1.7.0 מאת [`Amlaach`](https://github.com/Amlaach/ZerachExplorer)**  
   בהמשך לפיתוח של אביי, נוספה שכבת הקשחה, ניהול ומודרניזציה מקיפה (שלבים 0–7):
   * **אבטחה עמוקה (`PathPolicy`):** חסימת עקיפות דרך קישורים סימבוליים וצמתים (Symlinks / Junctions), חסימת נתיבי רשת UNC (`\\server\share`), נתיבי התקנים (`\\.\`), שמות DOS שמורים (`CON`, `NUL`, `LPT1`), נעילת סיומת בשינוי שם, ומחיקה בטוחה לסל המיחזור.
   * **ניהול קיוסק ופרופילים:** 4 פרופילי עבודה (`Standard`, `ReadOnly`, `Controlled`, `Custom`), הרשאות פעולה פרטניות (`PathPermissions`), תצורה מוגנת ב-`ProgramData`, ומסך הגדרות מנהל מוגן בסיסמת **PBKDF2** (`Ctrl+Shift+A`).
   * **פעולות קבצים ו-USB:** העתקה/גזירה/הדבקה (`Ctrl+C`/`X`/`V`) עם אימות כפול, בחירה מרובה, יצירת תיקייה חדשה (`Ctrl+Shift+N`), דיאלוג פתרון התנגשויות, הוצאה בטוחה של כונני USB (`DriveEjectService`), ודיאלוג USB מהיר בחיבור התקן.
   * **חוויית משתמש (UX):** סרגל פירורי לחם אינטראקטיבי, חיפוש וסינון בזמן אמת, מיון רב-עמודות, רענון אוטומטי (`FileSystemWatcher` + `WM_DEVICECHANGE`), תצוגה מקדימה מובנית ומבודדת (`Alt+P`), ותצוגת גריד/אריחים גדולים (`Ctrl+Shift+V`).
   * **נעילת קיוסק, ביקורת ופרטיות:** מניעת יציאה ללא סיסמת מנהל (`KioskController`), יומן ביקורת ופעילות (`AuditService`), ואיפוס סשן + ניקוי לוח העתקה (`SessionService`) בניתוק USB.
   * **מודרניזציה ו-CI/CD:** שדרוג מלא ל-**.NET 8 (LTS)** ו-C# 12, אינטגרציה עם `CommunityToolkit.Mvvm`, סוויטת בדיקות אוטומטית מקיפה, אוטומציית GitHub Actions (בנייה, בדיקות, SHA-256 והפצה), והפקת קובץ הפעלה יחיד ועצמאי (`Single-File Self-Contained`).

---

## 🔒 תכונות אבטחה מרכזיות

* **מודל רשימה לבנה (Drive Whitelist):** חשיפה כברירת מחדל של כוננים נשלפים (USB) בלבד; חסימת כוננים פנימיים ורשת.
* **חסימת כונן המערכת (`C:`):** חסימה דינמית שאינה תלויה ברישיות (`c:\`, `C:\`, נתיב Windows דינמי).
* **חסימת כונני "אוצר החוכמה":** זיהוי וחסימה לפי תווית כונן, תוכן פיזי (`otzar.exe`) ומזהי Volume Serial.
* **שירות הרשאות מרכזי (`PathPolicy`):** אימות כל פעולת ניווט, פתיחה, העתקה, העברה, מחיקה, יצירת תיקייה ושינוי שם.
* **הגנה מפני עקיפות (Bypass Protection):** חסימת Reparse Points / Junctions / Symlinks המצביעים למיקומים חסומים, חסימת UNC ונרמול מלא לפני כל בדיקה.
* **פתיחת מסמכים מאושרים בלבד:** סיומות ברירת מחדל: `doc`, `docx`, `xls`, `xlsx`, `pdf`, `txt`, `csv`, `one`, `onetoc2` (ניתנות להתאמה במסך המנהל).

---

## ⌨️ קיצורי מקלדת עיקריים

| קיצור | פעולה |
| :--- | :--- |
| `Ctrl+C` / `Ctrl+X` / `Ctrl+V` | העתקה, גזירה והדבקה מאומתת מדיניות |
| `Ctrl+Shift+N` | יצירת תיקייה חדשה |
| `F2` | שינוי שם (תוך נעילת סיומת הקובץ) |
| `Delete` | מחיקה בטוחה לסל המיחזור |
| `F5` | רענון תיקייה |
| `Alt+P` | הצגה/הסתרה של חלונית תצוגה מקדימה מהירה |
| `Ctrl+Shift+V` | החלפה בין תצוגת פרטים (Details) לתצוגת אריחים (Tiles) |
| `Ctrl+Shift+A` | פתיחת מסך הגדרות מנהל (מוגן בסיסמה) |

---

## ⚠️ גבולות גזרה והקשחת עמדה ציבורית (חובה לקרוא)

זרח אקספלורר מהווה **שכבת נוחות וממשק קיוסק מבוקר** ברמת היישום.  
בעת פתיחת מסמך Word/Excel/PDF, מופעלת התוכנה החיצונית של מערכת ההפעלה, ודרכה קיימים תפריטי "שמור בשם" / "פתח קובץ" שנגישים לדיסק לפי הרשאות המשתמש ב-Windows.

לפיכך, בעמדה ציבורית **חובה** לשלב את התוכנה עם:
1. **חשבון משתמש מוגבל (Standard User)** ללא הרשאות מנהל.
2. **הגדרות GPO:** החלת `NoDrives` ו-`NoViewOnDrive` להסתרת וחסימת כוננים במערכת, וחסימת `cmd`/`powershell`.
3. **הרשאות NTFS** לקריאה בלבד בכוננים מקומיים והגבלת מאקרו ביישומי Office.

למידע מפורט ראו את מסמך האבטחה המלא: [SECURITY.md](SECURITY.md).

---

## 🛠️ בנייה, בדיקות והפצה (Build & Test)

דרישות קדם: Windows עם **.NET 8 SDK**.

```powershell
# שחזור תלויות ובניית הפתרון (כולל פרויקט הבדיקות)
dotnet restore LiteExplorer.sln
dotnet build LiteExplorer.sln --configuration Release --no-restore

# הרצת סוויטת הבדיקות האוטומטית
dotnet run --project LiteExplorer.Tests/LiteExplorer.Tests.csproj --configuration Release --no-build

# הפקת קובץ הפעלה בודד ועצמאי (Single-File Self-Contained) ל-win-x64
./scripts/build-standalone.ps1
```

התוצר העצמאי יופק תחת `publish-standalone/LiteExplorer.exe` ואינו דורש התקנת .NET Runtime בעמדות הקצה.

---

## 📄 רישיון וקרדיטים

* **פרויקט מקורי:** [tempous/LiteExplorer](https://github.com/tempous/LiteExplorer) — Copyright (c) 2022, `tempous`
* **הסבה ופיתוח ראשוני לעמדות ציבוריות (זרח אקספלורר v1.4.0):** [abaye123/ZerachExplorer](https://github.com/abaye123/ZerachExplorer) — מאת **אביי** ([abaye.co](https://abaye.co))
* **הרחבה, הקשחת אבטחה ומודרניזציה ל-.NET 8 (v1.5.0–v1.7.0):** [Amlaach/ZerachExplorer](https://github.com/Amlaach/ZerachExplorer) — מאת **Amlaach**
* קוד המקור זמין תחת רישיון [BSD 3-Clause License](LICENSE).
