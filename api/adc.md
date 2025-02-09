# adc - 数模转换

{bdg-success}`已适配` {bdg-primary}`Air101/Air103` {bdg-primary}`Air601` {bdg-primary}`Air105` {bdg-primary}`ESP32C3` {bdg-primary}`ESP32S3` {bdg-primary}`Air780E/Air700E`

```{note}
本页文档由[这个文件](https://gitee.com/openLuat/LuatOS/tree/master/luat/modules/luat_lib_adc.c)自动生成。如有错误，请提交issue或帮忙修改后pr，谢谢！
```

```{tip}
本库有专属demo，[点此链接查看adc的demo例子](https://gitee.com/openLuat/LuatOS/tree/master/demo/adc)
```

## 常量

|常量|类型|解释|
|-|-|-|
|adc.ADC_RANGE_3_6|number|air105的ADC分压电阻开启，范围0~3.76V|
|adc.ADC_RANGE_1_8|number|air105的ADC分压电阻关闭，范围0~1.88V|
|adc.ADC_RANGE_3_8|number|air780E开启ADC0,1分压电阻，范围0~3.8V|
|adc.ADC_RANGE_1_2|number|air780E关闭ADC0,1分压电阻，范围0~1.2V|
|adc.CH_CPU|number|CPU内部温度的通道id|
|adc.CH_VBAT|number|VBAT供电电压的通道id|
|adc.T1|number|ADC1 (如存在多个adc可利用此常量使用多ADC 例如 adc.open(ADC1+2) 打开ADC1 channel 2)|
|adc.T2|number|ADC2 (如存在多个adc可利用此常量使用多ADC 例如 adc.open(ADC2+3) 打开ADC2 channel 3)|


## adc.open(id)



打开adc通道

**参数**

|传入值类型|解释|
|-|-|
|int|通道id,与具体设备有关,通常从0开始|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|打开结果|

**例子**

```lua
-- 打开adc通道4,并读取
if adc.open(4) then
    log.info("adc", adc.read(4)) -- 返回值有2个, 原始值和计算值,通常只需要后者
    log.info("adc", adc.get(4))  -- 返回值有1个, 仅计算值
end
adc.close(4) -- 若需要持续读取, 则不需要close, 功耗会高一点.

```

---

## adc.setRange(range)



设置ADC的测量范围，注意这个和具体芯片有关，目前只支持air105/Air780E系列

**参数**

|传入值类型|解释|
|-|-|
|int|range参数,与具体设备有关,比如air105填adc.ADC_RANGE_1_8和adc.ADC_RANGE_3_6|
|return|nil|

**返回值**

无

**例子**

```lua
-- 关闭air105内部分压
adc.setRange(adc.ADC_RANGE_1_8)
-- 打开air105内部分压
adc.setRange(adc.ADC_RANGE_3_6)

```

---

## adc.read(id)



读取adc通道

**参数**

|传入值类型|解释|
|-|-|
|int|通道id,与具体设备有关,通常从0开始|

**返回值**

|返回值类型|解释|
|-|-|
|int|原始值,一般没用,可以直接抛弃|
|int|从原始值换算得出的实际值，通常单位是mV|

**例子**

```lua
-- 打开adc通道2,并读取
if adc.open(2) then
    -- 这里使用的是adc.read会返回2个值, 推荐走adc.get函数,直接取实际值
    log.info("adc", adc.read(2))
end
adc.close(2)

```

---

## adc.get(id)



获取adc计算值

**参数**

|传入值类型|解释|
|-|-|
|int|通道id,与具体设备有关,通常从0开始|

**返回值**

|返回值类型|解释|
|-|-|
|int|单位通常是mV, 部分通道会返回温度值,单位千分之一摄氏度. 若读取失败,会返回-1|

**例子**

```lua
-- 本API 在 2022.10.01后编译的固件可用
-- 打开adc通道2,并读取
if adc.open(2) then
    log.info("adc", adc.get(2))
end
adc.close(2) -- 按需关闭

```

---

## adc.close(id)



关闭adc通道

**参数**

|传入值类型|解释|
|-|-|
|int|通道id,与具体设备有关,通常从0开始|

**返回值**

无

**例子**

```lua
-- 打开adc通道2,并读取
if adc.open(2) then
    log.info("adc", adc.read(2))
end
adc.close(2)

```

---

