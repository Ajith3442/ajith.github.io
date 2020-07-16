<html>

<head>
  <title>Parse CSV DATA</title>
  <style>
    .inputData {
      width: 100%;
      height: 200px;
      border-radius: 4px;
    }
    
    .outputData {
      width: 100%;
      height: 200px;
      border-radius: 4px;
    }
  </style>
</head>

<body>
  input <br>
  <textarea class="inputData" name="inputData" id="inputData" onchange="parseData()"></textarea> <br> output <br>
  <textarea class="outputData" name="outputData" id="outputData" disabled></textarea>

</body>

<script>
  parseData();

  function parseData() {
    var dataArray = [{
      'Id': 1000,
      'ParentId': null,
      'Name': 'Foo1000',
      'Description': 'Foo1000 node'
    }, {
      'Id': 700,
      'ParentId': 500,
      'Name': 'Foo700',
      'Description': 'Foo700 node'
    }, {
      'Id': 900,
      'ParentId': 100,
      'Name': 'Foo900',
      'Description': 'Foo900 node'
    }, {
      'Id': 500,
      'ParentId': 600,
      'Name': 'Foo500',
      'Description': 'Foo500 node'
    }, {
      'Id': 100,
      'ParentId': null,
      'Name': 'Foo100',
      'Description': 'Foo100 node'
    }, {
      'Id': 1100,
      'ParentId': 200,
      'Name': 'Foo1100',
      'Description': 'Foo1100 node'
    }, {
      'Id': 1100,
      'ParentId': 200,
      'Name': 'Foo1100',
      'Description': 'Foo1100 node'
    }, {
      'Id': 800,
      'ParentId': 500,
      'Name': 'Foo800',
      'Description': 'Foo800 node'
    }, {
      'Id': 200,
      'ParentId': 100,
      'Name': 'Foo200',
      'Description': 'Foo200 node'
    }, {
      'Id': 300,
      'ParentId': 1100,
      'Name': 'Foo300',
      'Description': 'Foo300 node'
    }, {
      'Id': 400,
      'ParentId': 200,
      'Name': 'Foo400',
      'Description': 'Foo400 node'
    }, {
      'Id': 600,
      'ParentId': 100,
      'Name': 'Foo600',
      'Description': 'Foo600 node'
    }];

    document.getElementById('inputData').value = JSON.stringify(dataArray);

    var outputArray = [];
    outputArray = setParetIdData(dataArray, null);
    document.getElementById('outputData').value = JSON.stringify(outputArray);

  }

  function setParetIdData(dataArray, key) {
    let response = {};
    // console.log(key);
    var subArray = dataArray.filter(d => d.ParentId === key);
    // console.log(subArray);
    if (subArray && Array.isArray(subArray) && subArray.length > 0) {
      subArray.forEach(ele => {
        childrenData = setParetIdData(dataArray, ele.Id);
        if (childrenData && Object.keys(childrenData).length > 0) {
          response[ele.Id] = {
            'name': ele.Name,
            'description': ele.Description,
            'children': childrenData
          };
        } else {
          response[ele.Id] = {
            'name': ele.Name,
            'description': ele.Description,
          };
        }
      });
    }
    return response;
  }
</script>

</html>
