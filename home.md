# Home

## Filters

To get filters we call

```
/dataprocessing/api/v1.0/SalePortal/groups
```

with specific header **_teamreferer: ofoodo_**

<details>
    <summary>Response is the list of portal types</summary>

```ts
0: {$id: "1", id: "0427d48d-2199-4080-a97b-c6983c5d7ce7",…}
    $id: "1"
    checkoutTypes: []
    code: "tags"
    directories: [,…]
    0: {$id: "6", id: "8e9c60b7-40a7-41cb-8fc0-054439125319", groupId: "0427d48d-2199-4080-a97b-c6983c5d7ce7",…}
        $id: "6"
        childCount: 0
        childrens: []
        code: "tags1"
        groupId: "0427d48d-2199-4080-a97b-c6983c5d7ce7"
        hasChild: false
        icon: ""
        id: "8e9c60b7-40a7-41cb-8fc0-054439125319"
        isActive: false
        name: {$id: "7", key: "8e9c60b7-40a7-41cb-8fc0-054439125319",…}
        parentId: null
        picture: ""
        priority: 0
    1: {$id: "10", id: "df49808f-8bdd-4311-9a5c-f3e578625ffe",…}
    2: {$id: "14", id: "37c74d0d-88e1-496e-bb46-d08db686b09b",…}
    3: {$id: "18", id: "85fe46ff-a584-471e-aca1-f8b8f207b6ac",…}
    4: {$id: "22", id: "ecc836eb-1730-4dc4-84a9-d47334d827b8",…}
    5: {$id: "26", id: "ff50477a-642f-4a19-a35c-3a4aca4c262b",…}
    6: {$id: "30", id: "71d6be09-1461-47f8-819f-e42cbe3b0b6f",…}
    7: {$id: "34", id: "a0766662-0c99-4730-aff8-0dd3a5857ea2",…}
    8: {$id: "38", id: "4b3d8c07-0048-48e5-ae84-c67c9bc96627",…}
    9: {$id: "42", id: "8972c961-1217-483b-ac56-e9f1c0b55404",…}
    10: {$id: "46", id: "66c04c0a-b73c-cd74-a093-ed1e807be8b7",…}
    icon: ""
    id: "0427d48d-2199-4080-a97b-c6983c5d7ce7"
    isActive: true
    isBase: true
    name: {$id: "2", key: "4d2c9ffd-4912-4b1e-9dc4-3d345d580985",…}
    $id: "2"
    key: "4d2c9ffd-4912-4b1e-9dc4-3d345d580985"
    translateParams: [{$id: "3", language: "ka", value: "პოპულარული კერძები"},…]
    picture: ""
    setting: {$id: "5", translateName: true, compareTeams: true, groupType: "Filter", selectionType: "Checkbox",…}
    $id: "5"
    compareTeams: true
    groupType: "Filter"
    selectionType: "Checkbox"
    translateName: true
    treeView: true
    sortIndex: 0
    type: "tags"
    typeId: 1
    typeKey: "4d2c9ffd-4912-4b1e-9dc4-3d345d580985"
    typeValue: "Filter"
```

</details>

<details>
    <summary>Classes structure we use in the ofoodo frontend</summary>

```ts
class PortalType {
  id: string;
  name: TranslatedTitleTypes;
  code: tFilterGroupCode;
  picture: string;
  icon: string;
  isActive: boolean;
  isBase: boolean;
  sortIndex: number;
  typeId: number;
  setting: TypeSettings;
  directories: Array<PortalTypeItem>;
}

class PortalTypeItem {
  id: string;
  groupId: string;
  name: TranslatedTitleTypes;
  code: string;
  isActive: boolean;
  picture: string;
  icon: string;
  parentId?: string;
  hasChild: boolean;
  priority: number;
  childCount: number;
  childrens?: PortalTypeItem[];
}

interface TypeSettings {
  translateName: boolean;
  compareTeam: boolean;
  groupType: string;
  selectionType: string;
  treeView: boolean;
}

interface TranslatedTitleTypes {
  key: string;
  translateParams: Array<{ language: string; value: string }>;
}

type tFilterGroupCode =
  | "restaurants"
  | "cuisines"
  | "locations"
  | "prices"
  | "seatingareas"
  | "tags";
```

</details>

## Sliders

To get portal grouped by types we call

```
/dataprocessing/api/v1.0/SalePortal/teamsgroups
```

with specific header **_teamreferer: ofoodo_**

Response is collection of such items

```json
{
    "count": 6,
    "data": [{$id: "4",…}, {$id: "111",…}, {$id: "204",…}, {$id: "281",…}, {$id: "361",…}, {$id: "438",…}],
    "groupCode": "discounts",
    "groupId": "32ffc243-e6d0-4df2-90eb-440d4f01aef3",
    "groupName": [{$id: "2", key: "e0df5c13-053d-490f-9603-a8278446829d", language: "ka", value: "ფასდაკლებები"},…],
    "message": "",
    "pageIndex": 0,
    "pageSize": -1,
    "success": true
}
```

where **_data_** is collection of portals
