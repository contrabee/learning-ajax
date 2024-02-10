<!doctype html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <title> jQuery Quiz</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>

    <style type="text/css">
        div.shittybike{
            margin: 10px 0 20px 0;
        }

        table {
            border: 1px solid;
            border-collapse: collapse;
        }

        td,
        th {
            padding: 10px;
            border: 1px solid;
        }

        .iloveyoubeech{
            color: red;
        }
    </style>

    <script>
        function b1(){
           $('#ta-ble').empty();
           $.ajax({
                type: "GET",
                url: "http://spartacodingclub.shop/sparta_api/citybike",
                data: {},
                success: function( response) {
                    let rows = response["getStationList"]["row"];
                    for (let i = 0; i < rows.length; i++){
                        let rackname = rows[i]['stationName'];
                        let rackcount= rows[i]['rackTotCnt'];
                        let bikecnt = rows[i]['parkingBikeTotCnt'];
                        let temp_html = '';
                        if (bikecnt<5){

                            temp_html = `<tr class="iloveyoubeech">
                                            <td>${rackname}</td>
                                            <td>${rackcount}</td>
                                            <td>${bikecnt}</td>
                                        </tr>`
                        } else {
                            temp_html = `<tr>
                                            <td>${rackname}</td>
                                            <td>${rackcount}</td>
                                            <td>${bikecnt}</td>
                                        </tr>`
                        } 
                        
                        $('#ta-ble').append(temp_html);
                    }
                }
           }) 
        }
    </script>



</head>
<body>
    <h1> Practice jQuery + Ajax</h1>
    
    <hr />

    <div class="shittybike">
        <h2>1. Practice using the CityBike API</h2>
        <p>Show me the current status of all the bikes</p>
        <p>Update the data below with the latest data everytime the "Update" button is pressed.</p>
        <button onclick="b1()">Update</button>
        <table>
            <thead>
                <tbody id="ta-ble">
                <tr>
                    <td> Bike stand location</td>
                    <td>Bike stand count </td>
                    <td>Parked bike count </td>
                </tr>

                <tr>
                    <td>102. Fun Fun st.</td>
                    <td>22</td>
                    <td>0</td>
                </tr>
                <tr>
                    <td>103. Happy Sad Ave.</td>
                    <td>16</td>
                    <td>0</td>
                </tr>
                <tr> 
                    <td>104. Potato Salami Dr.</td>
                    <td>16</td>
                    <td>0</td>
                </tr>
            </thead>
            </tbody>
        </table>
    </div>
</body>
</html>
