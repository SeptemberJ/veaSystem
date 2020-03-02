<template>
  <div class="Wallet">
    <div class="Wrap">
      <div class="AvailableBalance">
        <h5>可用余额</h5>
        <div class="TopSumary">
          <div class="TotalBalance"><span class="IntegralPart">5000.</span><span class="FractionalPart">00</span> 元</div>
          <div class="OptionBlock">
            <div class="Bt Recharge" @click="Recharge">充值</div>
            <div class="Bt CashWithdrawal">提现</div>
          </div>
          <div class="RightOptions">
            <span>对公转账汇款查询</span>
            <span class="MiddleBt">冻结余额详情</span>
            <span>费用预警</span>
          </div>
        </div>
      </div>
    </div>
    <div class="BalanceDetail">
      <div class="DetailItem">
        <span>总计余额</span>
        <span>7000.00 元</span>
      </div>
      <div class="DetailItem Symbol"> = </div>
      <div class="DetailItem">
        <span>可用余额</span>
        <span>5000.00 元</span>
      </div>
      <div class="DetailItem Symbol"> + </div>
      <div class="DetailItem">
        <span>冻结余额</span>
        <span>2000.00 元</span>
      </div>
    </div>
    <div class="Others">
      <el-row>
        <el-col :span="8">
          <div class="OthersItem" style="border-left:0;padding-left:0;">
            <div>对公账户</div>
            <div><span class="Number">0</span><span>个</span></div>
            <div>去认证企业对公账户</div>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="OthersItem">
            <div>优惠券</div>
            <div><span class="Number">0</span><span>张</span></div>
            <div>去使用优惠券</div>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="OthersItem">
            <div>积分</div>
            <div><span class="Number">0</span><span>分</span></div>
            <div>去兑换积分</div>
          </div>
        </el-col>
      </el-row>
    </div>
    <myDialog :dialog-visible="dialogVisible" title="对公账户充值汇款" @closeDialog="closeDialog">
      <div class="MainContent">
        <div class="InnerWrap">
          <div class="TopBlock" />
          <div class="TabBlock">
            <div class="Tabs">
              <span :class="{'active': tabIdx == 0}" @click="changeTab(0)">在线充值</span>
              <span :class="{'active': tabIdx == 1}" @click="changeTab(1)">对公汇款</span>
            </div>
            <div class="Bts">
              <span>充值记录</span>
              <span>对公汇款查询</span>
            </div>
          </div>
          <div class="MainBlock">
            <div v-if="tabIdx == 0">
              <div class="RechargeOnline">
                <el-form ref="form" :model="form" label-position="left" label-width="100px">
                  <el-form-item label="充值账户">
                    <span>上海AAA国际贸易有限公司</span>
                  </el-form-item>
                  <el-form-item label="可用余额">
                    <span>5000.00 元</span><span class="TipsTxt">（充值金额消费后才能开具发票）</span>
                  </el-form-item>
                  <el-form-item label="充值金额">
                    <el-input v-model="form.RechargeNumber" type="number" placeholder="请输入充值金额" style="width: 250px;margin-right: 10px;" />元
                  </el-form-item>
                  <el-form-item>
                    <el-button type="primary">立即充值</el-button>
                    <!-- <el-button v-waves type="primary">立即充值</el-button> -->
                    <!-- <a class="pan-btn blue-btn">立即充值</a> -->
                  </el-form-item>
                </el-form>
              </div>
            </div>
            <div v-else>
              <div class="RemittanceEnquiry" />
            </div>
          </div>
        </div>
      </div>
    </myDialog>
  </div>
</template>
<script>
import MyDialog from '@/components/MyDialog'
// import waves from '@/directive/waves/index.js'
export default {
  name: 'Wallet',
  components: {
    MyDialog
    // MDinput
  },
  // directives: {
  //   waves
  // },
  data() {
    return {
      dialogVisible: false,
      wid: '',
      tabIdx: 0,
      form: {
        RechargeNumber: ''
      }
    }
  },
  created() {
  },
  methods: {
    Recharge() {
      this.dialogVisible = true
    },
    changeTab(type) {
      this.tabIdx = type
    },
    closeDialog() {
      setTimeout(() => { this.dialogVisible = false }, 600)
    }
  }
}
</script>

<style lang="scss" scoped>
  $primaryBlue: #2196F3;
  $sideWidth: 180px;
  .Wallet{
    width: 100%;
    .Wrap{
      width: 100%;
      border-bottom: 1px solid #dfdfdf;
      background: #ffffff;
    }
    .AvailableBalance{
      padding: 20px 40px;
      .TopSumary{
        height: 80px;
        line-height: 80px;
        .TotalBalance{
          display: inline-block;
          float: left;
          .IntegralPart{
            font-size: 36px;
            color: $primaryBlue;
          }
          .FractionalPart{
            font-size: 28px;
            color: $primaryBlue;
          }
        }
        .OptionBlock{
          display: inline-block;
          float: left;
          margin-left: 40px;
          .Bt{
            width: 100px;
            height: 34px;
            line-height: 34px;
            font-size: 13px;
            text-align: center;
            display: inline-block;
            float: left;
            margin-top: 23px;
            cursor: pointer;
          }
          .Recharge{
            background: $primaryBlue;
            color: #ffffff;
          }
          .CashWithdrawal{
            border: 1px solid #7F7F7F;
            color: #7F7F7F;
            margin-left: 20px;
          }
        }
        .RightOptions{
          float:left;
          display: inline-block;
          margin-left: 40px;
          padding-top: 10px;
          font-size: 14px;
          color: $primaryBlue;
          span{
            cursor: pointer;
          }
          .MiddleBt::before{
            content: '';
            width: 1px;
            height: 14px;
            background: #7F7F7F;
            display: inline-block;
            margin-left: 10px;
            margin-right: 10px;
          }
          .MiddleBt::after{
            content: '';
            width: 1px;
            height: 14px;
            background: #7F7F7F;
            display: inline-block;
            margin-left: 10px;
            margin-right: 10px;
          }
        }
      }
    }
    .BalanceDetail{
      height: 80px;
      padding: 15px 40px;
      background: #ffffff;
      .DetailItem{
        width: 100px;
        height: 50px;
        float: left;
        display: inline-block;
        color: #333333;
        span{
          width: 100%;
          height: 25px;
          text-align: left;
          font-size: 14px;
          float: left;
        }
      }
      .Symbol{
        width: 50px;
        text-align: center;
        line-height: 50px;
        margin-right: 25px;
      }
    }
    .Others{
      padding: 20px 40px;
      height: 140px;
      background: #ffffff;
      margin-top: 20px;
      .OthersItem{
        width: 100%;
        height: 100px;
        font-size: 14px;
        color: #555555;
        border-left: 2px solid #dfdfdf;
        padding-left: 20px;
        div{
          width: 100%;
          height: 60px;
          display: block;
          .Number{
            height: 60px;
            font-size: 28px;
            line-height: 60px;
            margin-right: 10px;
          }
          &:first-of-type{
            height: 20px;
            line-height: 20px;
          }
          &:last-of-type{
            height: 20px;
            line-height: 20px;
            color: $primaryBlue;
            cursor: pointer;
            font-size: 12px;
          }
        }
      }
    }
    .MainContent{
      width: 100%;
      height: 100%;
      .TipsTxt{
        color: #F59A23;
      }
      .InnerWrap{
        height: 100%;
        padding: 10px 20px;
        .TopBlock{
          width: 100%;
          height: 100px;
          margin: 10px auto 20px auto;
          background: #E8F0FE;
          border: 1px solid #02a7f0;
        }
        .TabBlock{
          width: 100%;
          height: 60px;
          margin: 20px auto;
          background: #ffffff;
          .Tabs{
            float: left;
            & span{
              height: 50px;
              line-height: 70px;
              text-align: center;
              float: left;
              color: #7F7F7F;
              margin-left: 20px;
              cursor: pointer;
            }
            & .active{
              color: #000000;
              border-bottom: 2px solid #000000;
            }
          }
          .Bts{
            float: right;
            height: 60px;
            & span{
              width: 120px;
              height: 34px;
              display: inline-block;
              border: 1px solid #d7d7d7;
              color: #7F7F7F;
              font-size: 13px;
              margin: 13px 20px 13px 0;
              text-align: center;
              line-height: 34px;
              cursor: pointer;
            }
          }
        }
        .MainBlock{
          padding: 20px;
          margin: 20px auto 10px auto;
          background: #ffffff;
          color: #333333;
          .el-button{
            border-radius: 0px;
            width: 250px;
          }
        }
      }
    }
  }
</style>

