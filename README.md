### xlsmapper
---
http://mygreen.github.io/xlsmapper/sphinx/index.html

https://github.com/mygreen/xlsmapper

```java
@XlsSheet(name="List")
public class UserSheet {
  @XlsLabelCell(label="Date", type=LabelledCellType.Right)
  Date createDate;
  
  @XlsHorizontalRecords(tableLabel="User List")
  List<UserRecord> users;
}

public class UserRecord {
  @XlsColumn(columnName="ID")
  int no;
  @XlsColumn(columnName="Class", merged=true)
  String className;
  @XlsColumn(columnName="Name")
  String name;
  @XlsColumn(columnName="Gender")
  Gender gender;
}

public enum Gender {
  male, female;
}

XlsMapper xlsMapper = new XlsMapper();
UserSheet sheet = xlsMapper.load(
  new FileInputStream("example.xls"),
  UserSheet.class
);


@XlsSheet(name="List")
public class UserSheet {
  @XlsLabelledCell(label="Date", type=LabelledCellType.Right)
  @XlsDateTimeConverter(excelPattern="yyy/m/d")
  Date createDate;
  
  @XlsHorizontalRecords(tableLabel="User List")
  @XlsRecordOpton(overOperation=OverOperation.Insert)
  List<UserRecord> users;
}


UserSheet sheet = new UserSheet();
sheet.date = new Date();

List<UserRecord> users = new ArrayList<>();

UserRecord record1 = new UserRecord();
record1.no = 1;
record1.className = "A";
record1.name = "Ichiro";
record1.gender = Gender.male;
users.add(record1);

UserRecord record2 = new UserRecord();
users.add(record2);
sheet.users = users;
XlsMapper xlsMapper = new XlsMapper();
xlsMapper.save(
  new FileInputStream("template.xls"),
  new FileOutputStream("out.xls"),
  sheet
);
```

```sh
pip install sphinx
pip install sphinx_rtd_theme --upgrade
pip install janome
mvn clean package
mvn site -Dgpg.skip=true
```

```
```
