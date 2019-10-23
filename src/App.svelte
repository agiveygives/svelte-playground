<script>
  export let name;
  let headers = '';
  let data = '';

  import Table from './components/table/table.svelte';

  const processData = (data, headers) => {
    if (headers.length <= 0) return [];
    if (data.length <= 0) return [];

    const dataRows = data.split("\n");
    const headersList = headers.split(',')
    dataRows.forEach((rowData, index) => {
      let data = rowData.split(';');
      dataRows[index] = {}

      headersList.forEach((header, i) => {
        dataRows[index][header] = data[i]
      })
    })

    return dataRows;
  }
</script>

<span>
  Headers:
  <input type="text" bind:value={headers} />
</span>

<p>Row Data:</p>
<textarea bind:value={data} />


<div>
  <Table
    isLoading={false}
    headers={headers !== '' ? headers.split(',') : []}
    data={processData(data, headers)}
  />
</div>
