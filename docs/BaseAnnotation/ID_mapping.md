---
datatable: true
layout: page
parent: BaseAnnotation
title: ID_mapping
---

{% assign mydata=site.data.ID_mapping %} 
{: .note-title } 
>ID mapping
>
>A file or table that maps data identifiers to one another for example to establish a link between two biological databases for the purposes of data integration. [[Source]](http://edamontology.org/operation_3282)
<table id="myTable" class="display" style="width:100%">
    <thead>
    {% for column in mydata[0] %}
        <th>{{ column[0] }}</th>
    {% endfor %}
    </thead>
    <tbody>
    {% for row in mydata %}
        <tr>
        {% for cell in row %}
            <td>{{ cell[1] }}</td>
        {% endfor %}
        </tr>
    {% endfor %}
    </tbody>
</table>
<script type="text/javascript">
  $('#myTable').DataTable({
    responsive: {
        details: {
            display: $.fn.dataTable.Responsive.display.modal( {
                header: function ( row ) {
                    var data = row.data();
                    return 'Details for '+data[0];
                }
            } ),
            renderer: $.fn.dataTable.Responsive.renderer.tableAll({
                tableClass: "table"
            })
        }
    },
   "deferRender": true,
   "columnDefs": [
      { 
         targets: [3],
         render : function(data, type, row, meta){
            if(type === 'display' & data != 'Sage Bionetworks'){
               return $('<a>')
                  .attr('href', data)
                  .text(data)
                  .wrap('<div></div>')
                  .parent()
                  .html();} 
            if(type === 'display' & data == 'Sage Bionetworks'){
                return $('<a>')
                   .attr('href', 'https://sagebionetworks.org/')
                   .text(data)
                   .wrap('<div></div>')
                   .parent()
                   .html();
            
            } else {
               return data;
            }
         }
      } 
   ]
});
</script>