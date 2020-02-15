# Datatable plugin

* controller
* service
* javascript
* blade 

## Controller

```php
public function listArea(Request $request, AreaService $areaService){

        $mParam = array(
            'orderColumnName' => ($request->get('orderColumnName') == "") ? 'name' : $request->get('orderColumnName'),
            'orderType' => ($request->get('orderType') == "") ? 'asc' : $request->get('orderType'),
            'size' => ($request->get('size')  == "") ? 10 : $request->get('size'),
            'search' => $request->get('search')
        );

        $data = $areaService->findArea($mParam);

        $mData = array(
            'draw' => 0,
            'recordsTotal' => $data->perPage(),
            'recordsFiltered' =>  $data->total(),
            'data' => $data->items()
        );

        return $mData;
    }
```

## Service

```php
public function findArea($param){
        $areas = Area::where('name', 'LIKE',"%".$param['search']."%")->orderBy($param['orderColumnName'],$param['orderType'])->paginate($param['size']);
        return $areas;
    }
```

## Javascript

```js
var oTable = $('#area-datatable').DataTable({
        "processing": true,
        "serverSide": true,
        "ajax": {
                url : 'area/list.json',
                type: 'GET',
                data: function(d){
                var oTable = $('#area-datatable').DataTable();
                var info = oTable.page.info();
                var selectedColumn = oTable;
                // //                /*-------- paging number and showing current data ----------- */
                d.page = (info.page+1); // get current page
                d.size = d.length; // show entries
                // //                /*--------- Sorting Data ------------*/
                //                 //get index selected order
                var idxColumn = oTable.order()[0][0];
                //                 //get type selected order
                var idxType = oTable.order()[0][1];
                //                 d.myorder = d.columns[idxColumn].data+ ',' + idxType;

                //                 /*--------- search data ------------------- */
                d.search = d.search.value;
                d.orderColumnName = d.columns[idxColumn].data;
                d.orderType = idxType;

                }
        },
        "columns": [
                    { "data": "name" },
                    { "data": "description" }
                ],
        });
```

## Blade



