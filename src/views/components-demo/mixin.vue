<template>
  <div class="mixin-components-container">
    <el-row>
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>Buttons</span>
        </div>
        <div style="margin-bottom:50px;">
          <el-col :span="6" class="text-center">
            <router-link class="pan-btn light-blue-btn" to="/icon/index">
              Icons
            </router-link>
          </el-col>
          <el-col :span="6" class="text-center">
            <router-link class="pan-btn green-btn" to="/table/complex-table">
              Table
            </router-link>
          </el-col>
          <el-col :span="6" class="text-center">
            <router-link class="pan-btn tiffany-btn" to="/example/create">
              Form
            </router-link>
          </el-col>
          <el-col :span="6" class="text-center">
            <router-link class="pan-btn yellow-btn" to="/theme/index">
              Theme
            </router-link>
          </el-col>
        </div>
      </el-card>
    </el-row>

    <el-row :gutter="20" style="margin-top:50px;">
      <el-col :span="6">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>输入框</span>
          </div>
          <div style="height:100px;">
            <el-form :model="demo" :rules="demoRules">
              <el-form-item prop="title">
                <md-input v-model="demo.title" icon="search" name="title" placeholder="输入标题">
                  标题
                </md-input>
              </el-form-item>
            </el-form>
          </div>
        </el-card>
      </el-col>

      <el-col :span="6">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>图片hover效果</span>
          </div>
          <div class="component-item">
            <pan-thumb width="100px" height="100px" image="https://wpimg.wallstcn.com/577965b9-bb9e-4e02-9f0c-095b41417191">
              vue-element-admin
            </pan-thumb>
          </div>
        </el-card>
      </el-col>

      <el-col :span="6">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>水波纹 v指令</span>
          </div>
          <div class="component-item">
            <el-button v-waves type="primary">
              水波纹效果
            </el-button>
            <el-button v-waves type="primary" class="pan-btn green-btn">动画效果</el-button>
          </div>
        </el-card>
      </el-col>

      <el-col :span="6">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>滑入文字变形</span>
          </div>
          <div class="component-item">
            <mallki class-name="mallki-text" text="vue-element-admin" />
          </div>
        </el-card>
      </el-col>
    </el-row>

    <el-row :gutter="20" style="margin-top:50px;">
      <el-col :span="8">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>Share</span>
          </div>
          <div class="component-item" style="height:420px;">
            <dropdown-menu :items="articleList" style="margin:0 auto;" title="系列文章" />
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import PanThumb from '@/components/PanThumb'
import MdInput from '@/components/MDinput'
import Mallki from '@/components/TextHoverEffect/Mallki'
import DropdownMenu from '@/components/Share/DropdownMenu'
import waves from '@/directive/waves/index.js' // 水波纹指令
export default {
  name: 'ComponentMixinDemo',
  components: {
    PanThumb,
    MdInput,
    Mallki,
    DropdownMenu
  },
  directives: {
    waves
  },
  data() {
    const validate = (rule, value, callback) => {
      if (value.length !== 6) {
        callback(new Error('请输入六个字符'))
      } else {
        callback()
      }
    }
    return {
      demo: {
        title: ''
      },
      demoRules: {
        title: [{ required: true, trigger: 'change', validator: validate }]
      },
      articleList: [
        { title: 'javascript基础', href: 'javascript:;' },
        { title: 'javascript进阶', href: 'javascript:;' },
        { title: 'javascript中级', href: 'javascript:;' },
        { title: 'javascript高级', href: 'javascript:;' },
        { title: 'javascript专家', href: 'javascript:;' },
        { title: '全栈', href: 'javascript:;' }
      ]
    }
  }
}
</script>

<style scoped>
.mixin-components-container {
  background-color: #f0f2f5;
  padding: 30px;
  min-height: calc(100vh - 84px);
}
.component-item{
  min-height: 100px;
}
</style>
