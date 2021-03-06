---
title: Performance
summary: Rules that flag suboptimal code.
permalink: pmd_rules_apex_performance.html
folder: pmd/rules/apex
sidebaractiveurl: /pmd_rules_apex.html
editmepath: ../pmd-apex/src/main/resources/category/apex/performance.xml
keywords: Performance, AvoidDmlStatementsInLoops, AvoidSoqlInLoops, AvoidSoslInLoops
language: Apex
---
## AvoidDmlStatementsInLoops

**Since:** PMD 5.5.0

**Priority:** Medium (3)

Avoid DML statements inside loops to avoid hitting the DML governor limit. Instead, try to batch up the data into a list and invoke your DML once on that list of data outside the loop.

**This rule is defined by the following Java class:** [net.sourceforge.pmd.lang.apex.rule.performance.AvoidDmlStatementsInLoopsRule](https://github.com/pmd/pmd/blob/master/pmd-apex/src/main/java/net/sourceforge/pmd/lang/apex/rule/performance/AvoidDmlStatementsInLoopsRule.java)

**Example(s):**

``` java
public class Something {
    public void foo() {  
        for (Integer i = 0; i < 151; i++) {
            Account account;
            // ...
            insert account;
        }
    }
}
```

**This rule has the following properties:**

|Name|Default Value|Description|
|----|-------------|-----------|
|cc_categories|[Style]|Code Climate Categories|
|cc_remediation_points_multiplier|1|Code Climate Remediation Points multiplier|
|cc_block_highlighting|false|Code Climate Block Highlighting|

**Use this rule by referencing it:**
``` xml
<rule ref="category/apex/performance.xml/AvoidDmlStatementsInLoops" />
```

## AvoidSoqlInLoops

**Since:** PMD 5.5.0

**Priority:** Medium (3)

New objects created within loops should be checked to see if they can created outside them and reused.

**This rule is defined by the following Java class:** [net.sourceforge.pmd.lang.apex.rule.performance.AvoidSoqlInLoopsRule](https://github.com/pmd/pmd/blob/master/pmd-apex/src/main/java/net/sourceforge/pmd/lang/apex/rule/performance/AvoidSoqlInLoopsRule.java)

**Example(s):**

``` java
public class Something {
    public static void main( String as[] ) {
        for (Integer i = 0; i < 10; i++) {
            List<Account> accounts = [SELECT Id FROM Account];
        }
    }
}
```

**This rule has the following properties:**

|Name|Default Value|Description|
|----|-------------|-----------|
|cc_categories|[Style]|Code Climate Categories|
|cc_remediation_points_multiplier|1|Code Climate Remediation Points multiplier|
|cc_block_highlighting|false|Code Climate Block Highlighting|

**Use this rule by referencing it:**
``` xml
<rule ref="category/apex/performance.xml/AvoidSoqlInLoops" />
```

## AvoidSoslInLoops

**Since:** PMD 6.0.0

**Priority:** Medium (3)

Sosl calls within loops can cause governor limit exceptions.

**This rule is defined by the following Java class:** [net.sourceforge.pmd.lang.apex.rule.performance.AvoidSoslInLoopsRule](https://github.com/pmd/pmd/blob/master/pmd-apex/src/main/java/net/sourceforge/pmd/lang/apex/rule/performance/AvoidSoslInLoopsRule.java)

**Example(s):**

``` java
public class Something {
    public static void main( String as[] ) {
        for (Integer i = 0; i < 10; i++) {
            List<List<SObject>> searchList = [FIND 'map*' IN ALL FIELDS RETURNING Account (Id, Name), Contact, Opportunity, Lead];
        }
    }
}
```

**This rule has the following properties:**

|Name|Default Value|Description|
|----|-------------|-----------|
|cc_categories|[Style]|Code Climate Categories|
|cc_remediation_points_multiplier|1|Code Climate Remediation Points multiplier|
|cc_block_highlighting|false|Code Climate Block Highlighting|

**Use this rule by referencing it:**
``` xml
<rule ref="category/apex/performance.xml/AvoidSoslInLoops" />
```

