<template>
  <div class="HomePage">
    <div class="TopPart">
      <div class="FileNameOutbox">
        <div class="Title">文件名称:</div>
        <el-input v-model="FileName"></el-input>
      </div>
      <div class="TextareaOutbox">
        <el-input
          type="textarea"
          :autosize="{ minRows: 2, maxRows: 20 }"
          placeholder="请输入内容"
          v-model="ShowListData"
        >
        </el-input>
      </div>
    </div>
    <div class="BottomPart">
      <div class="ButtonOutbox">
        <el-button type="primary" @click="InitDataFun">生成数据</el-button>
        <el-button type="primary" @click="saveJSON(ShowListData, `${FileName}.json`)"
          >下载数据</el-button
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomePage",
  data() {
    return {
      FileName: "JsToJsonFile",
      ShowListData: "",
      ListData: [],
    };
  },
  mounted() {
    //this.InitDataFun();
  },
  methods: {
    saveJSON(data, filename) {
      if (!data) {
        alert("保存的数据为空");
        return;
      }
      if (!filename) filename = "json.json";
      if (typeof data === "object") {
        data = JSON.stringify(data, undefined, 4);
      }
      var blob = new Blob([data], { type: "text/json" }),
        e = document.createEvent("MouseEvents"),
        a = document.createElement("a");
      a.download = filename;
      a.href = window.URL.createObjectURL(blob);
      a.dataset.downloadurl = ["text/json", a.download, a.href].join(":");
      e.initMouseEvent(
        "click",
        true,
        false,
        window,
        0,
        0,
        0,
        0,
        0,
        false,
        false,
        false,
        false,
        0,
        null
      );
      a.dispatchEvent(e);
    },
    /************************以下是生成数据方法***********************************/
    InitDataFun() {
      let ListData = [];
      let FirstContentData = [];
      let SecondContentData = [];
      let ThirdContentData = [];
      let FourContentData = [];
      for (var i = 0; i < 16; i++) {
        if (i < 6) {
          FirstContentData.push({
            Name: "一级水厂" + (i + 1),
            Label: "一级水厂" + (i + 1),
            Status: 0,
            Msg: [],
            IsFather: true,
            Depth: 1,
            Time: "13:0" + i,
            Id: "Firstid" + (i + 1),
            LID: "Firstlid" + (i + 1),
            List: [
              {
                Title: "浊度",
                Data: 0.23,
              },
              {
                Title: "PH",
                Data: 3,
              },
              {
                Title: "湿度",
                Data: 0.63,
              },
              {
                Title: "COD",
                Data: 0.23,
              },
            ],
          });
          let ListDataSec = [];
          for (var Seci = 0; Seci < 16; Seci++) {
            let ListDatarsd = [];
            for (var Rsdi = 0; Rsdi < 16; Rsdi++) {
              let ListDataFour = [];
              for (var Fouri = 0; Fouri < 16; Fouri++) {
                ListDataFour.push({
                  Name: "四级水厂" + (Fouri + 1),
                  Label: "四级水厂" + (Fouri + 1),
                  Status: 1,
                  Msg: [],
                  IsFather: false,
                  Depth: 4,
                  Time: "13:0" + Fouri,
                  Id: "Fourid" + (Fouri + 1),
                  LID: "Fourlid" + (Fouri + 1),
                  ShowCode:
                    "一级---" +
                    (i + 1) +
                    "---二级---" +
                    (Seci + 1) +
                    "---三级---" +
                    (Rsdi + 1) +
                    "---四级---" +
                    (Fouri + 1),
                  Children: [],
                  List: [
                    {
                      Title: "浊度",
                      Data: 0.23,
                    },
                    {
                      Title: "PH",
                      Data: 3,
                    },
                    {
                      Title: "湿度",
                      Data: 0.63,
                    },
                    {
                      Title: "COD",
                      Data: 0.23,
                    },
                  ],
                });
              }
              ListDatarsd.push({
                Name: "三级水厂" + (Rsdi + 1),
                Label: "三级水厂" + (Rsdi + 1),
                Status: 1,
                Msg: [],
                IsFather: true,
                Depth: 3,
                Time: "13:0" + Rsdi,
                Id: "Thirdid" + (Rsdi + 1),
                LID: "Thirdlid" + (Rsdi + 1),
                ShowCode:
                  "一级---" +
                  (i + 1) +
                  "---二级---" +
                  (Seci + 1) +
                  "---三级---" +
                  (Rsdi + 1),
                Children: ListDataFour,
                List: [
                  {
                    Title: "浊度",
                    Data: 0.23,
                  },
                  {
                    Title: "PH",
                    Data: 3,
                  },
                  {
                    Title: "湿度",
                    Data: 0.63,
                  },
                  {
                    Title: "COD",
                    Data: 0.23,
                  },
                ],
              });
            }
            ListDataSec.push({
              Name: "二级水厂" + (Seci + 1),
              Label: "二级水厂" + (Seci + 1),
              Status: 0,
              Msg: [],
              IsFather: true,
              Depth: 2,
              Time: "13:0" + Seci,
              Id: "Secondid" + (Seci + 1),
              LID: "Secondlid" + (Seci + 1),
              ShowCode: "一级---" + (i + 1) + "---二级---" + (Seci + 1),
              Children: ListDatarsd,
              List: [
                {
                  Title: "浊度",
                  Data: 0.23,
                },
                {
                  Title: "PH",
                  Data: 3,
                },
                {
                  Title: "湿度",
                  Data: 0.63,
                },
                {
                  Title: "COD",
                  Data: 0.23,
                },
              ],
            });
          }
          ListData.push({
            Name: "一级水厂" + (i + 1),
            Label: "一级水厂" + (i + 1),
            Status: 0,
            Msg: [],
            IsFather: true,
            Depth: 1,
            Time: "13:0" + i,
            Id: "Firstid" + (i + 1),
            LID: "Firstlid" + (i + 1),
            ShowCode: "一级---" + (i + 1),
            List: [
              {
                Title: "浊度",
                Data: 0.23,
              },
              {
                Title: "PH",
                Data: 3,
              },
              {
                Title: "湿度",
                Data: 0.63,
              },
              {
                Title: "COD",
                Data: 0.23,
              },
            ],
            Children: ListDataSec,
          });
        }
        SecondContentData.push({
          Name: "二级水厂" + (i + 1),
          Label: "二级水厂" + (i + 1),
          Status: 0,
          Msg: [],
          IsFather: true,
          Depth: 2,
          Time: "13:0" + i,
          Id: "Secondid" + (i + 1),
          LID: "Secondlid" + (i + 1),
          List: [
            {
              Title: "浊度",
              Data: 0.23,
            },
            {
              Title: "PH",
              Data: 3,
            },
            {
              Title: "湿度",
              Data: 0.63,
            },
            {
              Title: "COD",
              Data: 0.23,
            },
          ],
        });
        ThirdContentData.push({
          Name: "三级水厂" + (i + 1),
          Label: "三级水厂" + (i + 1),
          Status: 1,
          Msg: [],
          IsFather: true,
          Depth: 3,
          Time: "13:0" + i,
          Id: "Thirdid" + (i + 1),
          LID: "Thirdlid" + (i + 1),
          List: [
            {
              Title: "浊度",
              Data: 0.23,
            },
            {
              Title: "PH",
              Data: 3,
            },
            {
              Title: "湿度",
              Data: 0.63,
            },
            {
              Title: "COD",
              Data: 0.23,
            },
          ],
        });
        FourContentData.push({
          Name: "四级水厂" + (i + 1),
          Label: "四级水厂" + (i + 1),
          Status: 1,
          Msg: [],
          IsFather: false,
          Depth: 4,
          Time: "13:0" + i,
          Id: "Fourid" + (i + 1),
          LID: "Fourlid" + (i + 1),
          List: [
            {
              Title: "浊度",
              Data: 0.23,
            },
            {
              Title: "PH",
              Data: 3,
            },
            {
              Title: "湿度",
              Data: 0.63,
            },
            {
              Title: "COD",
              Data: 0.23,
            },
          ],
        });
      }
      this.FirstContentData = FirstContentData;
      this.SecondContentData = SecondContentData;
      this.ThirdContentData = ThirdContentData;
      this.FourContentData = FourContentData;
      this.ListData = SecondContentData;
      this.ShowListData = JSON.stringify(SecondContentData);
      // console.log("ListData",ListData)
      //console.log("JSON.stringify(ListData)", JSON.stringify(ListData));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.HomePage {
  width: 100%;
  height: 100%;
  .TopPart {
    width: 100%;
    /*  height: 80%; */
    .FileNameOutbox {
      display: flex;
      flex-flow: row nowrap;
      align-items: center;
      width: 20%;
      margin-top: 30px;
      margin-left: 20px;
      .Title {
        margin-right: 10px;
        white-space: nowrap;
      }
    }
    .TextareaOutbox {
      width: calc(100% - 40px);
      // height: calc(100% - 20px);
      // border: 1px solid #666;
      // box-sizing: border-box;
      margin-bottom: 30px;
      margin-top: 20px;
      margin-left: 20px;
    }
  }
  .BottomPart {
    display: flex;
    flex-flow: row nowrap;
    justify-content: center;
    align-items: center;
    width: 100%;
    /* height: 20%; */
    .ButtonOutbox {
      display: flex;
      flex-flow: row nowrap;
      justify-content: center;
      align-items: center;
      width: calc(100% - 20px);
      // height: calc(100% - 20px);
      // border: 1px solid #666;
      // box-sizing: border-box;
    }
  }
}
</style>
