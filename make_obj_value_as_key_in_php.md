``` php

$jsonResponse =  '[{
		"Postleitzahl": 9651,
		"Ort": "Ennetbühl",
		"Kanton": "SG"
	},
	{
		"Postleitzahl": 9652,
		"Ort": "Neu St. Johann",
		"Kanton": "SG"
	},
	{
		"Postleitzahl": 9655,
		"Ort": "Stein SG",
		"Kanton": "SG"
	},
	{
		"Postleitzahl": 9656,
		"Ort": "Alt St. Johann",
		"Kanton": "SG"
	},
	{
		"Postleitzahl": 9657,
		"Ort": "Unterwasser",
		"Kanton": "SG"
	},
	{
		"Postleitzahl": 9658,
		"Ort": "Wildhaus",
		"Kanton": "SG"
	}
]';


$data = json_decode($jsonResponse, true);

$result = array();

foreach ($data as $item) {
    $postleitzahl = $item["Postleitzahl"];
    $ort = $item["Ort"];
    $kanton = $item["Kanton"];

    $result[$postleitzahl] = array(
        "ort" => $ort,
        "kanton" => $kanton
    );
}

//[9658] => Array
       // (
       //     [ort] => Wildhaus
        //    [kanton] => SG
       // )

// Print the resulting array
print_r(json_encode($result));
```
