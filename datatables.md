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

## Blade



