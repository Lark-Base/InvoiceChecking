<template>
  <div class = "center">

    <el-link href="https://dac57ho49r5.feishu.cn/docx/MG5KdjT5lo5fTOxLoNBcRIFTnYc" target="_blank"><el-text tag="b">{{ $t('form.appCode') }}</el-text></el-link>
    
    <el-text>{{ $t('form.feishuDocument') }}</el-text>
    
    <el-link href="https://bytedance.larkoffice.com/docx/WXtGdRmOioeH9VxlfCtc1Y41nKe" target="_blank"><el-text tag="b">{{ $t('form.plugIn') }}</el-text></el-link>
    
    <el-text style="margin-top: 10px;">{{ $t('form.defaultcode') }}</el-text>
    
    <el-skeleton style="display: flex;justify-content: center;" :loading="appcodeLoading" animated>
      <template #template>
        <el-skeleton-item style="width: 80%;height: 20px;" />
      </template>
      <template #default>
        <el-text>{{ defaultAppCode }}</el-text>
      </template>
    </el-skeleton>

    <el-text>{{ $t('form.remain') }}</el-text>

    <el-skeleton style="display: flex;justify-content: center;" :loading="remainLoading" animated>
      <template #template>
        <el-skeleton-item style="width: 15%;height: 20px;" />
      </template>
      <template #default>
        <el-text>{{ remain }}</el-text>
      </template>
    </el-skeleton>

    <el-input style="margin-top: 5px;" v-model="input" type="password" :placeholder="$t('form.enterAppcode')" show-password/>

    <div style="width: 100%;display: flex;flex-direction: row;">
      <el-popover width="200px" placement="top-start" :title="$t(`form.content.unneccessary`)" :width="400" trigger="hover" :content="$t(`form.content.fpdmRemind`)">
        <template #reference>
          <el-text style="margin-top: 20px;" size="default">{{ $t('form.content.fpdmTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select style="width: 100%;margin-top: 5px;" v-model="fpdmContent" :placeholder="$t(`form.content.textSelect`)" size="large" :no-data-text="$t(`form.content.noField`)">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click = "fpdmRenew(item)"/>
    </el-select>

    <div style="width: 100%;display: flex;flex-direction: row;">
      <el-popover width="200px" placement="top-start" :title="$t(`form.content.neccessary`)" :width="400" trigger="hover" :content="$t(`form.content.fphmRemind`)">
        <template #reference>
          <el-text style="margin-top: 20px;" size="default">{{ $t('form.content.fphmTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select style="width: 100%;margin-top: 5px;" v-model="fphmContent" :placeholder="$t(`form.content.textSelect`)" size="large" :no-data-text="$t(`form.content.noField`)">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click = "fphmRenew(item)" />
    </el-select>
    
    <div style="width: 100%;display: flex;flex-direction: row;">
      <el-popover width="200px" placement="top-start" :title="$t(`form.content.unneccessary`)" :width="400" trigger="hover" :content="$t(`form.content.xymRemind`)">
        <template #reference>
          <el-text style="margin-top: 20px;" size="default">{{ $t('form.content.xymTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select style="width: 100%;margin-top: 5px;" v-model="xymContent" :placeholder="$t(`form.content.textSelect`)" size="large" :no-data-text="$t(`form.content.noField`)">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click = "xymRenew(item)"/>
    </el-select>

    <div style="width: 100%;display: flex;flex-direction: row;">
      <el-popover width="200px" placement="top-start" :title="$t(`form.content.neccessary`)" :width="400"  trigger="hover" :content="$t(`form.content.kprqRemind`)">
        <template #reference>
          <el-text style="margin-top: 20px;" size="default">{{ $t('form.content.kprqTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select style="width: 100%;margin-top: 5px;" v-model="kprqContent" :placeholder="$t(`form.content.dateSelect`)" size="large" :no-data-text="$t(`form.content.noField`)">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click = "kprqRenew(item)"/>
    </el-select>

    <div style="width: 100%;display: flex;flex-direction: row;">
      <el-popover width="200px" placement="top-start" :title="$t(`form.content.unneccessary`)" :width="400" trigger="hover" :content="$t(`form.content.bhsjeRemind`)">
        <template #reference>
          <el-text style="margin-top: 20px;" size="default" >{{ $t('form.content.bhsjeTitle') }}</el-text>
        </template>
      </el-popover>
    </div>
    <el-select style="width: 100%;margin-top: 5px;" v-model="bhsjeContent" :placeholder="$t(`form.content.moneySelect`)" size="large" :no-data-text="$t(`form.content.noField`)">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click = "bhsjeRenew(item)"/>
    </el-select>

    <el-text style="width: 100%;margin-top: 20px;" size="default">{{ $t('form.content.yzTitle') }}</el-text>
    <el-select style="width: 100%;margin-top: 5px;" v-model="yzContent" :placeholder="$t(`form.content.pleaseSelect`)" size="large" :no-data-text="$t(`form.content.noField`)">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click = "yzRenew(item)"/>
    </el-select>

    <el-text style="width: 100%;margin-top: 20px;" size="default">{{ $t('form.content.zfTitle') }}</el-text>
    <el-select style="width: 100%;margin-top: 5px;" v-model="zfContent" :placeholder="$t(`form.content.pleaseSelect`)" size="large" :no-data-text="$t(`form.content.noField`)">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click = "zfRenew(item)"/>
    </el-select>

    <el-text style="width: 100%;margin-top: 20px;" size="default">{{ $t('form.content.chTitle') }}</el-text>
    <el-select style="width: 100%;margin-top: 5px;" v-model="chContent" :placeholder="$t(`form.content.pleaseSelect`)" size="large" :no-data-text="$t(`form.content.noField`)">
      <el-option v-for="item in fieldList" :key="item.id" :value="item.name" @click = "chRenew(item)"/>
    </el-select>

    <el-button type="success" :disabled = "able" @click="submitData" style="width: 100%;margin-top: 23px;">{{ $t('form.content.submit') }}</el-button>
  </div>
</template>


<script setup>
import { ref,onMounted,h,watch } from 'vue';
import { bitable} from '@lark-base-open/js-sdk';
import  axios  from 'axios';
import { ElMessage,ElNotification} from 'element-plus';
import { useI18n } from 'vue-i18n';
import useCurrentInstance from "./useCurrentInstance";
import { useStorage } from '@vueuse/core'

const  {proxy}  = useCurrentInstance();
const { t } = useI18n();
let locale = 'zh'
const selection = ref({})
const records = ref([])

let fieldList = []
let testList = []

const fpdmContent = useStorage('fpdmContent','')
const fphmContent = useStorage('fphmContent','')
const kprqContent = useStorage('kprqContent','')
const xymContent = useStorage('xymContent','')
const bhsjeContent = useStorage('bhsjeContent','')
const yzContent = useStorage('yzContent','')
const zfContent = useStorage('zfContent','')
const chContent = useStorage('chContent','')


const input = useStorage('appcode','')
const remain = ref('获取中')
const defaultAppCode = ref('获取中')
let appcodeLoading = ref(true)
let remainLoading = ref(true)


const able = ref(false)
const codeFieldId = useStorage('codeFieldId','')
const numFieldId = useStorage('numFieldId','')
const checkFieldId = useStorage('checkFieldId','')
const sumFieldId = useStorage('sumFieldId','')
const dateFieldId = useStorage('dateFieldId','')
const yzFieldId = useStorage('yzFieldId','')
const zfFieldId = useStorage('zfFieldId','')
const chFieldId = useStorage('chFieldId','')

const viewId = useStorage('vid','')


const fpdmRenew = (item)=>{
  fpdmContent.value = item.name
  codeFieldId.value = item.id
}

const fphmRenew = (item)=>{
  fphmContent.value = item.name
  numFieldId.value = item.id
}

const xymRenew = (item)=>{
  xymContent.value = item.name
  checkFieldId.value = item.id
}

const kprqRenew = (item)=>{
  kprqContent.value = item.name
  dateFieldId.value = item.id
}

const bhsjeRenew = (item)=>{
  bhsjeContent.value = item.name
  sumFieldId.value = item.id
}

const yzRenew = (item)=>{
  yzContent.value = item.name
  yzFieldId.value = item.id
}

const zfRenew = (item)=>{
  zfContent.value = item.name
  zfFieldId.value = item.id

}

const chRenew = (item)=>{
  chContent.value = item.name
  chFieldId.value = item.id
}

const successBox = (e) => {
  if(locale == 'zh'){
    ElMessage({
      message: '发票号码'+e+'核验正确',
      type: 'success',
    })
  }else{
    ElMessage({
      message: 'Invoice number'+e+'verified to be correct',
      type: 'success',
    })
  }
}

const warningBox = (e) => {
  if(locale == 'zh'){
    ElMessage({
      message: '发票号码'+e+'核验错误',
      type: 'warning',
    })
  }else{
    ElMessage({
      message: 'Invoice number'+e+'verified to be wrong',
      type: 'warning',
    })
  }
}

const errorBox = (e) => {
  if(locale == 'zh'){
    ElMessage.error('发票号码'+e.num +'获取数据失败('+e.message+')')
  }else{
    ElMessage.error('Invoice number'+e.num +'failed to obtain data('+e.message+')')
  }
}

const formPrompt = () => {
  if(locale == 'zh'){
    ElNotification({
      title: '提示',
      message: h('i', { style: 'color: black' }, '请完整填写列表'),
    })
  }else{
    ElNotification({
      title: 'Prompt',
      message: h('i', { style: 'color: black' }, 'Please fill out the complete list'),
    })
  }
}

const codePrompt = () => {
  if(locale == 'zh'){
    ElNotification({
      title: '提示',
      message: h('i', { style: 'color: black' }, '请填写AppCode'),
   })
  }else{
    ElNotification({
      title: 'Prompt',
      message: h('i', { style: 'color: black' }, 'Please fill in AppCode'),
   })
  }
}

onMounted(async () => {
  
  fetchRemain()
  
  setTimeout(() => {
    locale = proxy.$message.global.locale
  }, 1000);

  bitable.base.onSelectionChange(() => {
    reloadData()
  })

  reloadData()

})

watch(defaultAppCode,()=>{
  appcodeLoading.value = false
})

watch(remain,()=>{
  remainLoading.value = false
})

const fetchRemain = ()=>{
  axios.get('https://833zkqa1m6.us.aircode.run/hello')
    .then((res)=>{
      remain.value = res.data.result.Result.filter(r=>r.ProductCode == "cmapi00050226")[0].TotalQuota
      defaultAppCode.value = res.data.message
    })
    .catch((err)=>{
      remain.value = 0
      defaultAppCode.value = err.data.message
    })
}


const reloadData = async() =>{
  selection.value = await bitable.base.getSelection();
  if (viewId.value != selection.value.viewId) {
    viewId.value = selection.value.viewId
    codeFieldId.value = ''
    numFieldId.value = ''
    checkFieldId.value = ''
    sumFieldId.value = ''
    dateFieldId.value = ''
    yzFieldId.value = ''
    zfFieldId.value = ''
    chFieldId.value = ''
    fpdmContent.value = ''
    fphmContent.value = ''
    kprqContent.value = ''
    xymContent.value = ''
    bhsjeContent.value = ''
    yzContent.value = ''
    zfContent.value = ''
    chContent.value = ''
  }
  
  const table = await bitable.base.getTableById(selection.value.tableId)
  const view = await table.getViewById(selection.value.viewId);
  const fieldListId = await view.getVisibleFieldIdList()

  fieldList = []
  for (let element of fieldListId) {
    let fmeta = await table.getFieldMetaById(element)
    let newEle = {
      id:fmeta.id,
      name:fmeta.name
    }
    fieldList = fieldList.concat(newEle)
  }

  records.value = await view.getVisibleRecordIdList()

}

const submitData = async () => {
  if(input.value == ''){
    codePrompt()
  }else if(fpdmContent.value != '' &&fphmContent.value != '' && kprqContent.value != '' && xymContent.value != '' && bhsjeContent.value != '' && yzContent.value != '' && zfContent.value != '' && chContent.value != '' ){
    able.value = true
    
    const table = await bitable.base.getTableById(selection.value.tableId)
    const codeField = await table.getField(codeFieldId.value);
    const numField = await table.getField(numFieldId.value);
    const checkField = await table.getField(checkFieldId.value);
    const sumField = await table.getField(sumFieldId.value);
    const dateField = await table.getField(dateFieldId.value);
    const yzField = await table.getField(yzFieldId.value);
    const chField = await table.getField(chFieldId.value);
    const zfField = await table.getField(zfFieldId.value);
    
    for (let record of records.value) {

      let yzCell = await yzField.getCell(record);
      let yzRes = await yzCell.getValue();
      let yzVal = ''
      if (yzRes != null) {
        yzVal = yzRes[0].text
      }

      let chCell = await chField.getCell(record);
      let chRes = await chCell.getValue();
      let chVal = ''
      if (chRes != null) {
        chVal = chRes[0].text
      }

      let zfCell = await zfField.getCell(record);
      let zfRes = await zfCell.getValue();
      let zfVal = ''
      if (zfRes != null) {
        zfVal = zfRes[0].text
      }

      if (yzVal == '' && chVal == '' && zfVal == '') {
        let codeCell = await codeField.getCell(record);
        let codeRes = await codeCell.getValue();
        let codeVal = ''
        if(codeRes != null){
          codeVal = codeRes[0].text
        }
        let numCell = await numField.getCell(record);
        let numRes = await numCell.getValue();
        let numVal = ''
        if(numRes != null){
          numVal = numRes[0].text
        }
        let checkCell = await checkField.getCell(record);
        let checkRes = await checkCell.getValue();
        let checkVal = ''
        if(checkRes != null){
          checkVal = checkRes[0].text
        }
        let sumCell = await sumField.getCell(record);
        let sumRes = await sumCell.getValue();
        let sumVal = ''
        if (sumRes != null) {
          if (typeof sumRes == 'number') {
            sumVal = '' + sumRes
          }else{
            sumVal = sumRes[0].text.split('').filter(letter => !Number.isNaN(parseInt(letter)) || letter =='.').join('')
          }
        }
        let dateCell = await dateField.getCell(record);
        let dateRes = await dateCell.getValue();
        let dateVal = ''
        if(dateRes != null){
          if(typeof dateRes == 'number'){
            var date = new Date(dateRes);
            var Y = date.getFullYear();
            var M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1);
            var D = (date.getDate() < 10 ? '0' + (date.getDate()) : date.getDate());
            dateVal = ''+Y+M+D
          }else{
            dateVal = dateRes[0].text.split('').filter(letter => !Number.isNaN(parseInt(letter))).join('')
          }
        }
        let test = {
          recordId:record,
          codeVal:codeVal,
          numVal:numVal,
          checkVal:checkVal,
          sumVal:sumVal,
          dateVal:dateVal
        }
        testList = testList.concat(test)
        
      }
    }

    await requestData()

  }else{
    formPrompt()
  }
}

const requestData = async () => {
  const table = await bitable.base.getTableById(selection.value.tableId)
  
  for (let record of testList) {
    await axios({
      method:'post',
      url:'https://jminvoice.market.alicloudapi.com/invoice/validate',
      headers: { 
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8', 
        'Authorization': `APPCODE ${input.value}`, 
      },
      data : {
        fpdm:record.codeVal,
        fphm:record.numVal,
        kprq:record.dateVal,
        bhsje:record.sumVal,
        xym:record.checkVal
      }
    }).then(async (response) => {
      let message = ''
      let cancellationMark = ''
      let hcbz = ''
      if (response.data.data.message == '一致') {
        successBox(response.data.data.info.invoiceNo)
        if(locale == 'zh'){
          message = '一致'
        }else{
          message = 'Consistent'
        }
        if(response.data.data.info.cancellationMark == '0'){
          if(locale == 'zh'){
            cancellationMark = '未作废'
          }else{
            cancellationMark = 'Not Voided'
          }
        }else{
          if(locale == 'zh'){
            cancellationMark = '已作废'
          }else{
            cancellationMark = 'Voided'
          }
        }
        switch (response.data.data.info.hcbz) {
          case '0': 
            if(locale == 'zh'){
              hcbz = '未红冲'
            }else{
              hcbz = 'Unred Offset'
            }
          break;
          case '1': 
            if(locale == 'zh'){
              hcbz = '全额红冲'
            }else{
              hcbz = 'Full Red Offset'
            }
          break;
          case '2': 
            if(locale == 'zh'){
              hcbz = '部分红冲'
            }else{
              hcbz = 'Partial Red Offset'
            }
          break;
        }
      }else if(response.data.data.message == '不一致'){
          
          warningBox(record.numVal)
          if(locale == 'zh'){
              message = '不一致'
            }else{
              message = 'Inconsistent'
            }
      }
      await table.setCellValue(yzFieldId.value, record.recordId, message)
      await table.setCellValue(zfFieldId.value, record.recordId, cancellationMark)
      await table.setCellValue(chFieldId.value, record.recordId, hcbz)
    }).catch(async (err) => {

      let message = ''
      switch (err.message.split('').filter(letter => !Number.isNaN(parseInt(letter))).join('')) {
        case '203': 
          if(locale == 'zh'){
            message = '超过该张票当天查验次数，税局规定的每张发票一天只能调用5次'
          }else{
            message = 'If the number of inspections on the same day exceeds the limit, the tax bureau stipulates that each invoice can only be called 5 times a day'
          }
        break;
        case '204': 
          if(locale == 'zh'){
            message = '查验发票张数超过限制查验发票张数超过限制'
          }else{
            message = 'The number of verified invoices exceeds the limit'
          }
        break;
        case '205': 
          if(locale == 'zh'){
            message = '超过五年的发票不能查验，请核对开票日期是否正确'
          }else{
            message = 'Invoices over five years cannot be verified. Please verify if the invoicing date is correct'
          }
        break;
        case '206': 
          if(locale == 'zh'){
            message = '当前发票正在查验中,请稍后重试'
          }else{
            message = 'The current invoice is being verified, please try again later'
          }
        break;
        case '207': 
          if(locale == 'zh'){
            message = '该地区暂不支持该票种查验'
          }else{
            message = 'The region currently does not support verification of this ticket type'
          }
        break;
        case '400': 
          if(locale == 'zh'){
            message = '参数错误'
          }else{
            message = 'Parameter error'
          }
        break;
        case '411': 
          if(locale == 'zh'){
            message = '查询发票不规范, 请核对参数是否符合发票规范'
          }else{
            message = 'The invoice query is not standardized. Please verify if the parameters meet the invoice specifications'
          }
        break;
        case '412': 
          if(locale == 'zh'){
            message = '开票日期超过当前日期，请核对开票日期是否正确'
          }else{
            message = 'The invoicing date exceeds the current date. Please verify if the invoicing date is correct'
          }
        break;
        case '500': 
          if(locale == 'zh'){
            message = '服务商维护，请稍候再试'
          }else{
            message = 'Service provider maintenance, please try again later'
          }
        break;
        case '502':
          if(locale == 'zh'){
            message = '网络故障，请稍候再试'
          }else{
            message = 'Network malfunction, please try again later'
          } 
        break;
        default:
          if(locale == 'zh'){
            message = '请检查AppCode'     
          }else{
            message = 'Failed to obtain data, please check AppCode'
          } 
      }
      errorBox({message,
        num:record.numVal})

      if (message == '请检查AppCode' || message == 'Failed to obtain data, please check AppCode') {
        message = ''
      }

      await table.setCellValue(yzFieldId.value, record.recordId, message)
    })
  }

}

</script>


<style scoped>
.center {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;;
}
</style>
