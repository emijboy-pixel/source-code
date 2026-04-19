# source-code
function dailyHRReport() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Attendance");
  var data = sheet.getDataRange().getValues();

  var late = [];
  var absent = [];
  var overtime = [];

  for (var i = 1; i < data.length; i++) {

    var name = data[i][2];
    var status = data[i][5];
    var lateStatus = data[i][6];
    var hours = data[i][7];

    if (status == "Absent") {
      absent.push(name);
    }

    if (lateStatus == "Late") {
      late.push(name);
    }

    if (hours && hours > 10/24) {
      overtime.push(name);
    }
  }

  var message =
    "HR DAILY REPORT\n\n" +
    "Late:\n" + late.join("\n") +
    "\n\nAbsent:\n" + absent.join("\n") +
    "\n\nOvertime:\n" + overtime.join("\n");

  MailApp.sendEmail("hr@company.com", "Daily HR Report", message);
}
