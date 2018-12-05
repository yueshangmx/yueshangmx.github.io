---
layout: post
title: BootstrapValidator
date: 2018-12-05
description: "form，validator,bootstrap"
tags: 笔记   
---

### BootstrapValidator 详细配置

```javascript
////////////
/*settings */
////////////
	$(formSelector).bootstrapValidator({
//Form settings
		//指示错误消息的显示位置:CSS selector、tooltip、popover
		container:'#messages',
		//不会被验证的字段
	    excluded: [':disabled', ':hidden', ':not(:visible)', function($field, validator) {
		    		// $field 是jQuery对象表示field元素
		    	    // validator 是BootstrapValidator实例
		    	    // return true or false;
					// 不要验证不可见元素
				    return !$field.is(':visible');
				}],
		//字段校验图标。默认bootstrap图标
	    feedbackIcons: {
	        valid: 'glyphicon glyphicon-ok',
	        invalid: 'glyphicon glyphicon-remove',
	        validating: 'glyphicon glyphicon-refresh'
	    },
	    //字段的父元素:<td><input type="text" class="form-control" name="project[]" /></td>
	    group: 'td',
	    //实时验证模式
	    live: 'enabled',//enabled(实时验证),disabled(禁用实时验证,提交表单后才显示错误消息),submitted(提交表单后启用实时验证)
	    //所有字段的默认错误消息
	    message: '该值无效',
	    //表单输入无效时，禁用按钮,<span class="btn" id="submit"></span>(不使用button)
	    submitButtons: '#submit',
	    //字段长度小于设置的字符数，则不会对该字段进行实时验证。可以为特定字段设置此选项。
	    threshold:10,
	    //启用实时验证模式时触发的事件以验证所有字段。触发多个事件，则用空格分隔它们。
	    trigger: 'keyup',
	    //将符合的错误提示全部显示
	    verbose:true,//false:字段的验证将在第一次遇到错误时终止,即只显示当前的一个提示
//Field settings
	    fields: {
	    	firstName:{
	    		container: '#firstNameMessage',
	    		*enabled:Boolean,//启用或禁用字段验证
	    		excluded: Boolean,//是否排除该字段
	    		feedbackIcons:Boolean,//启用或禁用反馈图标,Form settings中为object
	    		group: String,
	    		message: String,
	    		*selector: '#firstName',//用于无法使用字段的name属性的情况
	    		threshold: Number,
	    		trigger: String,
	    		verbose: Boolean,
//Validator settings
	    		validators: {
	    		//内置验证器，详细实例见地址http://bootstrapvalidator.votintsev.ru/validators/
	    			//base64:{},//验证base64编码的字符串
	    			between: {},//检查输入值是否在两个给定数字之间,greaterThan:{},lessThan:{}
	    			callback: {//从回调方法返回有效性
                        callback: function (value, validator, $field) {
                            //value是字段的值
                            //validator是BootstrapValidator的实例
                            //$field是表示field元素的jQuery对象
                            //检查字段有效性
                            return true;    // or false
                        }
                    },
                    choice:{},//检查复选框的数量是否小于或大于给定数量
                    creditCard:{},//验证信用卡号
                    //cusip:{},//验证CUSIP
                    //cvv:{},//验证CVV编号
                    date:{},//验证日期
                    different:{},//如果输入值与给定字段的值不同，则返回true,例如要求用户名和密码不能相同
                    digits:{},//如果值仅包含数字，则返回true
                    //ean:{},//验证EAN（国际物品编号）
                    emailAddress:{},//验证电子邮件地址
                    file:{},//验证文件
                    greaterThan:{},//如果值大于或等于给定数字，则返回true
                    //grid:{},//验证GRId（全局发布标识符）
                    //hex:{},//验证十六进制数
                    //hexColor:{},//验证十六进制颜色
                    //iban:{},//验证国际银行帐号（IBAN）
                    //id:{},//验证标识号
                    identical:{},//检查该值是否与特定字段之一相同,例如二次密码输入校验是否输入相同
                    //imei:{},//验证IMEI（国际移动台设备标识）]
                    //imo:{},//验证IMO（国际海事组织）
                    integer:{},//验证整数
                    ip:{},//验证IP地址。支持IPv4和IPv6
                    //isbn:{},//验证ISBN（国际标准书号）。支持ISBN 10和ISBN 13
                    //isin:{},//验证ISIN（国际证券识别号码）
                    //ismn:{},//验证ISMN（国际标准音乐编号）
                    //issn:{},//验证ISSN（国际标准序列号）
                    lessThan:{},//如果值小于或等于给定数字，则返回true
                    //mac:{},//验证MAC地址
                    //meid:{},//验证MEID（移动设备标识符）
                    notEmpty: {},//检查值是否为空
                    numeric:{},//检查值是否为数字
                    phone:{},//验证电话号码
                    regexp:{},//检查值是否与给定的Javascript正则表达式匹配
                    remote:{},//通过Ajax请求执行远程检查
                    //rtn:{},//验证RTN（路由转接号码）
                    //sedol:{},//验证SEDOL（证券交易所每日官方名单）
                    //siren:{},//验证警报号码
                    //siret:{},//Validate a Siret number(不清楚是什么)
                    step:{},//检查值是否有效第一步
                    stringCase:{},//检查字符串是小写还是大写
                    stringLength:{},//验证字符串的长度
                    uri:{},//验证URL地址
                    uuid:{},//验证UUID，支持v3，v4，v5
                    vat:{},//验证增值税号
                    //vin:{},//验证美国VIN（车辆识别码）
                    zipCode:{},//验证邮政编码
                }
	    	}
	    }
	});
/////////////////////////////////////////////////////////////////////////
/*events,详细例子见http://bootstrapvalidator.votintsev.ru/settings/#events	*/ 
/////////////////////////////////////////////////////////////////////////
	$(formSelector).on('init.form.bv', function(e, data){
	//Form events
		// init.form.bv:在插件初始化表单后触发
		//error.form.bv:表单无效时触发
		//success.form.bv:表单有效时触发
		//added.field.bv:添加动态字段后触发
		//removed.field.bv:删除给定字段后触发
	//Field events
		//init.field.bv
		//error.field.bv:当某一字段无效时触发
		//success.field.bv:当某一字段有效时触发
		//status.field.bv:字段更改状态时触发,function(e, data){data.status}
			//每个字段有四种可能的状态：
			//NOT_VALIDATED该字段尚未验证
			//VALIDATING该字段正在验证中
			//INVALID该字段验证无效
			//VALID该字段验证有效
		$(formSelector).on('init.field.bv', '[name="email"]', function(e, data) {
            // 为特定字段触发事件
        })
    //Validator events
    	//error.validator.bv
    	//success.validator.bv
	});
		
	
 
 
	//等价于
	// <form data-bv-message="This value is not valid"
	//       data-bv-feedbackicons-valid="glyphicon glyphicon-ok"
	//       data-bv-feedbackicons-invalid="glyphicon glyphicon-remove"
	//       data-bv-feedbackicons-validating="glyphicon glyphicon-refresh"
	//       data-bv-submitbuttons='button[type="submit"]'
	//       data-bv-live="enabled">
	//     ...
	// </form>
	// $(document).ready(function() {
	//     $(formSelector).bootstrapValidator({
	//         fields: ...
	//     });
	// });
 
 

```

