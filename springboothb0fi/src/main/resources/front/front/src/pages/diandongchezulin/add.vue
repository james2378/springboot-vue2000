<template>
<div :style='{"width":"1200px","padding":"120px 7% 100px","margin":"0px auto","position":"relative","background":"url(http://codegen.caihongy.cn/20230109/138a4d606eae4a168810cef229969885.png) no-repeat center top,url(http://codegen.caihongy.cn/20230109/b95aeae1c1294f398aefb7c6cd5b16de.png) no-repeat center top,url(http://codegen.caihongy.cn/20230109/5ffc803e6682418eb7f0b09a98e35527.png) no-repeat center bottom,#faf0e6"}'>
    <el-form
      class="add-update-preview"
      ref="ruleForm"
      :model="ruleForm"
      :rules="rules"
      label-width="110px"
    >
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="订单编号" prop="dingdanbianhao">
              <el-input v-model="ruleForm.dingdanbianhao" placeholder="订单编号" readonly></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="电动车名称" prop="diandongchemingcheng">
            <el-input v-model="ruleForm.diandongchemingcheng" 
                placeholder="电动车名称" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="电动车品牌" prop="diandongchepinpai">
            <el-input v-model="ruleForm.diandongchepinpai" 
                placeholder="电动车品牌" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="图片" v-if="type!='cross' || (type=='cross' && !ro.tupian)" prop="tupian">
            <file-upload
            tip="点击上传图片"
            action="file/upload"
            :limit="3"
            :multiple="true"
            :fileUrls="ruleForm.tupian?ruleForm.tupian:''"
            @change="tupianUploadChange"
            ></file-upload>
          </el-form-item>
            <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' class="upload" v-else label="图片" prop="tupian">
                <img v-if="ruleForm.tupian.substring(0,4)=='http'" class="upload-img" style="margin-right:20px;" v-bind:key="index" :src="ruleForm.tupian.split(',')[0]" width="100" height="100">
                <img v-else class="upload-img" style="margin-right:20px;" v-bind:key="index" v-for="(item,index) in ruleForm.tupian.split(',')" :src="baseUrl+item" width="100" height="100">
            </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="电动车型号" prop="diandongchexinghao">
            <el-input v-model="ruleForm.diandongchexinghao" 
                placeholder="电动车型号" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="车牌号" prop="chepaihao">
            <el-input v-model="ruleForm.chepaihao" 
                placeholder="车牌号" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="日租价格" prop="rizujiage">
            <el-input v-model="ruleForm.rizujiage" 
                placeholder="日租价格" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="租赁日期" prop="zulinriqi" >
              <el-date-picker
                  format="yyyy 年 MM 月 dd 日"
                  value-format="yyyy-MM-dd"
                  v-model="ruleForm.zulinriqi" 
                  type="date"
                  placeholder="租赁日期">
              </el-date-picker> 
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="租赁天数" prop="zulintianshu">
            <el-input v-model="ruleForm.zulintianshu" 
                placeholder="租赁天数" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="总价格" prop="zongjiage">
              <el-input v-model="zongjiage" placeholder="总价格" readonly></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="账号" prop="zhanghao">
            <el-input v-model="ruleForm.zhanghao" 
                placeholder="账号" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="姓名" prop="xingming">
            <el-input v-model="ruleForm.xingming" 
                placeholder="姓名" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="联系方式" prop="lianxifangshi">
            <el-input v-model="ruleForm.lianxifangshi" 
                placeholder="联系方式" clearable ></el-input>
          </el-form-item>
          <el-form-item :style='{"padding":"10px","boxShadow":"0 2px 0 #efe4d4","margin":"0 0 10px"}' label="身份证号" prop="shenfenzhenghao">
            <el-input v-model="ruleForm.shenfenzhenghao" 
                placeholder="身份证号" clearable ></el-input>
          </el-form-item>

      <el-form-item :style='{"padding":"0","textAlign":"center","margin":"0"}'>
        <el-button :style='{"border":"0","cursor":"pointer","padding":"0","margin":"0 20px 0 0","outline":"none","color":"rgba(255, 255, 255, 1)","borderRadius":"4px","background":"#cca162","width":"128px","lineHeight":"40px","fontSize":"14px","height":"40px"}'  type="primary" @click="onSubmit">提交</el-button>
        <el-button :style='{"border":"0px solid rgba(64, 158, 255, 1)","cursor":"pointer","padding":"0","margin":"0","outline":"none","color":"#fff","borderRadius":"4px","background":"#009688","width":"128px","lineHeight":"40px","fontSize":"14px","height":"40px"}' @click="back()">返回</el-button>
      </el-form-item>
    </el-form>
</div>
</template>

<script>
  export default {
    data() {
      return {
        id: '',
        baseUrl: '',
        ro:{
            dingdanbianhao : false,
            diandongchemingcheng : false,
            diandongchepinpai : false,
            tupian : false,
            diandongchexinghao : false,
            chepaihao : false,
            rizujiage : false,
            zulinriqi : false,
            zulintianshu : false,
            zongjiage : false,
            zhanghao : false,
            xingming : false,
            lianxifangshi : false,
            shenfenzhenghao : false,
            ispay : false,
        },
        type: '',
        userTableName: localStorage.getItem('UserTableName'),
        ruleForm: {
          dingdanbianhao: this.getUUID(),
          diandongchemingcheng: '',
          diandongchepinpai: '',
          tupian: '',
          diandongchexinghao: '',
          chepaihao: '',
          rizujiage: '',
          zulinriqi: '',
          zulintianshu: '',
          zongjiage: '',
          zhanghao: '',
          xingming: '',
          lianxifangshi: '',
          shenfenzhenghao: '',
          ispay: '',
        },
        rules: {
          dingdanbianhao: [
          ],
          diandongchemingcheng: [
            { required: true, message: '电动车名称不能为空', trigger: 'blur' },
          ],
          diandongchepinpai: [
          ],
          tupian: [
          ],
          diandongchexinghao: [
          ],
          chepaihao: [
          ],
          rizujiage: [
            { required: true, message: '日租价格不能为空', trigger: 'blur' },
            { validator: this.$validate.isIntNumer, trigger: 'blur' },
          ],
          zulinriqi: [
          ],
          zulintianshu: [
            { validator: this.$validate.isIntNumer, trigger: 'blur' },
          ],
          zongjiage: [
            { validator: this.$validate.isIntNumer, trigger: 'blur' },
          ],
          zhanghao: [
            { required: true, message: '账号不能为空', trigger: 'blur' },
          ],
          xingming: [
          ],
          lianxifangshi: [
            { validator: this.$validate.isMobile, trigger: 'blur' },
          ],
          shenfenzhenghao: [
            { validator: this.$validate.isIdCard, trigger: 'blur' },
          ],
          ispay: [
          ],
        },
      };
    },
    computed: {


        zongjiage:{
            get: function () {
                return 1*this.ruleForm.rizujiage*this.ruleForm.zulintianshu
            }
        },

    },
    created() {
	  //this.bg();
      let type = this.$route.query.type ? this.$route.query.type : '';
      this.init(type);
      this.baseUrl = this.$config.baseUrl;
      this.ruleForm.zulinriqi = this.getCurDate()
    },
    methods: {
      getMakeZero(s) {
          return s < 10 ? '0' + s : s;
      },
      // 下载
      download(file){
        window.open(`${file}`)
      },
      // 初始化
      init(type) {
        this.type = type;
        if(type=='cross'){
          var obj = JSON.parse(localStorage.getItem('crossObj'));
          for (var o in obj){
            if(o=='dingdanbianhao'){
              this.ruleForm.dingdanbianhao = obj[o];
              this.ro.dingdanbianhao = true;
              continue;
            }
            if(o=='diandongchemingcheng'){
              this.ruleForm.diandongchemingcheng = obj[o];
              this.ro.diandongchemingcheng = true;
              continue;
            }
            if(o=='diandongchepinpai'){
              this.ruleForm.diandongchepinpai = obj[o];
              this.ro.diandongchepinpai = true;
              continue;
            }
            if(o=='tupian'){
              this.ruleForm.tupian = obj[o].split(",")[0];
              this.ro.tupian = true;
              continue;
            }
            if(o=='diandongchexinghao'){
              this.ruleForm.diandongchexinghao = obj[o];
              this.ro.diandongchexinghao = true;
              continue;
            }
            if(o=='chepaihao'){
              this.ruleForm.chepaihao = obj[o];
              this.ro.chepaihao = true;
              continue;
            }
            if(o=='rizujiage'){
              this.ruleForm.rizujiage = obj[o];
              this.ro.rizujiage = true;
              continue;
            }
            if(o=='zulinriqi'){
              this.ruleForm.zulinriqi = obj[o];
              this.ro.zulinriqi = true;
              continue;
            }
            if(o=='zulintianshu'){
              this.ruleForm.zulintianshu = obj[o];
              this.ro.zulintianshu = true;
              continue;
            }
            if(o=='zongjiage'){
              this.ruleForm.zongjiage = obj[o];
              this.ro.zongjiage = true;
              continue;
            }
            if(o=='zhanghao'){
              this.ruleForm.zhanghao = obj[o];
              this.ro.zhanghao = true;
              continue;
            }
            if(o=='xingming'){
              this.ruleForm.xingming = obj[o];
              this.ro.xingming = true;
              continue;
            }
            if(o=='lianxifangshi'){
              this.ruleForm.lianxifangshi = obj[o];
              this.ro.lianxifangshi = true;
              continue;
            }
            if(o=='shenfenzhenghao'){
              this.ruleForm.shenfenzhenghao = obj[o];
              this.ro.shenfenzhenghao = true;
              continue;
            }
          }
        }
        // 获取用户信息
        this.$http.get(this.userTableName + '/session', {emulateJSON: true}).then(res => {
          if (res.data.code == 0) {
            var json = res.data.data;
            if(json.chepaihao!=''&&json.chepaihao){
                this.ruleForm.chepaihao = json.chepaihao
            }
            if(json.zhanghao!=''&&json.zhanghao){
                this.ruleForm.zhanghao = json.zhanghao
            }
            if(json.xingming!=''&&json.xingming){
                this.ruleForm.xingming = json.xingming
            }
            if(json.lianxifangshi!=''&&json.lianxifangshi){
                this.ruleForm.lianxifangshi = json.lianxifangshi
            }
            if(json.shenfenzhenghao!=''&&json.shenfenzhenghao){
                this.ruleForm.shenfenzhenghao = json.shenfenzhenghao
            }
          }
        });
      },

    // 多级联动参数
      // 多级联动参数
      info(id) {
        this.$http.get('diandongchezulin/detail/${id}', {emulateJSON: true}).then(res => {
          if (res.data.code == 0) {
            this.ruleForm = res.data.data;
          }
        });
      },
      // 提交
      onSubmit() {

          this.ruleForm.zongjiage = this.zongjiage
        //更新跨表属性
        var crossuserid;
        var crossrefid;
        var crossoptnum;
        this.$refs["ruleForm"].validate(valid => {
          if(valid) {
            if(this.type=='cross'){
                 var statusColumnName = localStorage.getItem('statusColumnName');
                 var statusColumnValue = localStorage.getItem('statusColumnValue');
                 if(statusColumnName && statusColumnName!='') {
                     var obj = JSON.parse(localStorage.getItem('crossObj'));
                     if(!statusColumnName.startsWith("[")) {
                         for (var o in obj){
                             if(o==statusColumnName){
                                 obj[o] = statusColumnValue;
                             }
                         }
                         var table = localStorage.getItem('crossTable');
                         this.$http.post(table+'/update', obj).then(res => {});
                     } else {
                            crossuserid=Number(localStorage.getItem('userid'));
                            crossrefid=obj['id'];
                            crossoptnum=localStorage.getItem('statusColumnName');
                            crossoptnum=crossoptnum.replace(/\[/,"").replace(/\]/,"");
                     }
                 }
            }
            if(crossrefid && crossuserid) {
                 this.ruleForm.crossuserid=crossuserid;
                 this.ruleForm.crossrefid=crossrefid;
                 var params = {
                     page: 1,
                     limit: 10,
                     crossuserid:crossuserid,
                     crossrefid:crossrefid,
                 }
                 this.$http.get('diandongchezulin/list', {
                  params: params
                 }).then(res => {
                     if(res.data.data.total>=crossoptnum) {
                         this.$message({
                          message: localStorage.getItem('tips'),
                          type: 'success',
                          duration: 1500,
                         });
                          return false;
                     } else {
                         // 跨表计算


                          this.$http.post('diandongchezulin/add', this.ruleForm).then(res => {
                              if (res.data.code == 0) {
                                  this.$message({
                                      message: '操作成功',
                                      type: 'success',
                                      duration: 1500,
                                      onClose: () => {
                                          this.$router.go(-1);
                                      }
                                  });
                              } else {
                                  this.$message({
                                      message: res.data.msg,
                                      type: 'error',
                                      duration: 1500
                                  });
                              }
                          });
                     }
                 });
             } else {


                  this.$http.post('diandongchezulin/add', this.ruleForm).then(res => {
                     if (res.data.code == 0) {
                          this.$message({
                              message: '操作成功',
                              type: 'success',
                              duration: 1500,
                              onClose: () => {
                                  this.$router.go(-1);
                              }
                          });
                      } else {
                          this.$message({
                              message: res.data.msg,
                              type: 'error',
                              duration: 1500
                          });
                      }
                  });
             }
          }
        });
      },
      // 获取uuid
      getUUID () {
        return new Date().getTime();
      },
      // 返回
      back() {
        this.$router.go(-1);
      },
      tupianUploadChange(fileUrls) {
          this.ruleForm.tupian = fileUrls.replace(new RegExp(this.$config.baseUrl,"g"),"");;
      },
    }
  };
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
	.el-date-editor.el-input {
		width: auto;
	}
	
	.add-update-preview .el-form-item /deep/ .el-form-item__label {
	  padding: 0 10px 0 0;
	  color: #666;
	  font-weight: 500;
	  width: 110px;
	  font-size: 14px;
	  line-height: 40px;
	  text-align: right;
	}
	
	.add-update-preview .el-form-item /deep/ .el-form-item__content {
	  margin-left: 110px;
	}
	
	.add-update-preview .el-input /deep/ .el-input__inner {
	  border: 1px solid #e5d9c6;
	  border-radius: 4px;
	  padding: 0 12px;
	  outline: none;
	  color: #333;
	  width: 400px;
	  font-size: 14px;
	  height: 40px;
	}
	
	.add-update-preview .el-select /deep/ .el-input__inner {
	  border: 1px solid #e5d9c6;
	  border-radius: 4px;
	  padding: 0 10px;
	  outline: none;
	  color: #333;
	  width: 200px;
	  font-size: 14px;
	  height: 40px;
	}
	
	.add-update-preview .el-date-editor /deep/ .el-input__inner {
	  border: 1px solid #e5d9c6;
	  border-radius: 4px;
	  padding: 0 10px 0 30px;
	  outline: none;
	  color: #333;
	  width: 200px;
	  font-size: 14px;
	  height: 40px;
	}
	
	.add-update-preview /deep/ .el-upload--picture-card {
		background: transparent;
		border: 0;
		border-radius: 0;
		width: auto;
		height: auto;
		line-height: initial;
		vertical-align: middle;
	}
	
	.add-update-preview /deep/ .upload .upload-img {
	  border: 1px solid #e5d9c6;
	  cursor: pointer;
	  border-radius: 6px;
	  color: #333;
	  width: 100px;
	  font-size: 32px;
	  line-height: 100px;
	  text-align: center;
	  height: 100px;
	}
	
	.add-update-preview /deep/ .el-upload-list .el-upload-list__item {
	  border: 1px solid #e5d9c6;
	  cursor: pointer;
	  border-radius: 6px;
	  color: #333;
	  width: 100px;
	  font-size: 32px;
	  line-height: 100px;
	  text-align: center;
	  height: 100px;
	}
	
	.add-update-preview /deep/ .el-upload .el-icon-plus {
	  border: 1px solid #e5d9c6;
	  cursor: pointer;
	  border-radius: 6px;
	  color: #333;
	  width: 100px;
	  font-size: 32px;
	  line-height: 100px;
	  text-align: center;
	  height: 100px;
	}
	
	.add-update-preview .el-textarea /deep/ .el-textarea__inner {
	  border: 1px solid #e5d9c6;
	  border-radius: 4px;
	  padding: 12px;
	  outline: none;
	  color: #333;
	  width: 400px;
	  font-size: 14px;
	  height: 120px;
	}
</style>
