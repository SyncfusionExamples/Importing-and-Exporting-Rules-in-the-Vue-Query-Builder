<template>
  <div class="container">
    <div>
      <ejs-button cssClass="button" @click="importRules">Import Rules</ejs-button>
      <ejs-button cssClass="button" @click="exportRules">Export Rules</ejs-button>
    </div>
    <ejs-querybuilder :dataSource="dataSource" ref="querybuilder" />
  </div>
</template>
<script>
import { QueryBuilderComponent, QueryLibrary, QueryBuilder } from "@syncfusion/ej2-vue-querybuilder";
import { ButtonComponent } from "@syncfusion/ej2-vue-buttons";
QueryBuilder.Inject(QueryLibrary);

// #region hardwareData
var hardwareData = [{
  'TaskID': 1,
  'Name': 'Lenovo Yoga',
  'Category': 'Laptop',
  'SerialNo': 'CB27932009',
  'InvoiceNo': 'INV-2878',
  'Status': 'Assigned'
},
{
  'TaskID': 2,
  'Name': 'Acer Aspire',
  'Category': 'Others',
  'SerialNo': 'CB35728290',
  'InvoiceNo': 'INV-3456',
  'Status': 'In-repair'
},
{
  'TaskID': 3,
  'Name': 'Apple MacBook',
  'Category': 'Laptop',
  'SerialNo': 'CB35628728',
  'InvoiceNo': 'INV-2763',
  'Status': 'In-repair'
}];
// #endregion 

export default {
  components: {
    "ejs-querybuilder": QueryBuilderComponent,
    "ejs-button": ButtonComponent
  },
  data() {
    return {
      dataSource: hardwareData,
      rule: {
        'condition': 'or',
        'rules': [{
          'label': 'Category',
          'field': 'Category',
          'operator': 'equal',
          'value': 'Laptop'
        },
        {
          'condition': 'and',
          'rules': [{
            'label': 'Status',
            'field': 'Status',
            'operator': 'notequal',
            'value': 'Pending'
          },
          {
            'label': 'Task ID',
            'field': 'TaskID',
            'operator': 'equal',
            'value': 5675
          }]
        }]
      }
    };
  },
  methods: {
    importRules() {
      this.$refs.querybuilder.ej2Instances.setRules(this.rule);

      /*  this.$refs.querybuilder.ej2Instances.setRulesFromSql(
        "TaskID = 1 and Status LIKE ('Assigned%')"
      ); */

      /* this.$refs.querybuilder.ej2Instances.setParameterizedSql(
               {
                 sql: '(Category IN (?,?) OR TaskID IN (?,?))',
                 params: ['Laptop', 'Others', 1, 2]
               }); */
	  /* this.$refs.querybuilder.ej2Instances.setParameterizedNamedSql(
        {
          sql: '(Category IN (:Category_1,:Category_2) OR TaskID IN (:TaskID_1,:TaskID_2))',
          params: { "Category_1": "Laptop", "Category_2": "Others", "TaskID_1": 1, "TaskID_2": 2 }
        }
      ); */
    },
    exportRules() {
      console.log(

         this.$refs.querybuilder.ej2Instances.getValidRules()

         /* this.$refs.querybuilder.ej2Instances.getSqlFromRules(
        this.$refs.querybuilder.ej2Instances.getValidRules()) */

        /* this.$refs.querybuilder.ej2Instances.getParameterizedSql(
          this.$refs.querybuilder.ej2Instances.getValidRules()) */

          /* this.$refs.querybuilder.ej2Instances.getParameterizedNamedSql(
          this.$refs.querybuilder.ej2Instances.getValidRules()) */
      );
    }
  }
};
</script>

<style>
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-dropdowns/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-lists/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-calendars/styles/material.css";
@import "../node_modules/@syncfusion/ej2-vue-querybuilder/styles/material.css";

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 95%;
  margin: 0 auto;
  position: absolute;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
}

.button {
  margin: 20px;
}
</style>
