# android-pickers
# ��Ҫ
[![API 14+](https://img.shields.io/badge/API-14%2B-green.svg)](https://github.com/addappcn/android-pickers)


��׿ѡ������⣬�������ڼ�ʱ��ѡ�����������÷�Χ��������ѡ�������������Ա�ְҵ��ѧ���������ȣ������е�ַѡ��������ʡ�����ؼ����ؼ���������ѡ���������������䡢��ߡ����ء��¶ȵȣ��ȡ���
��ӭ������[Issues](https://github.com/addappcn/android-pickers/issues)�ύ���������顣
��ӭFork & Pull requests�������Ĵ��룬��ҹ�ͬѧϰ��android-pickers����Ⱥ : 456738690����
[�鿴������־](https://github.com/addappcn/android-pickers/blob/master/ChangeLog.md)

����ǻ���[Android-PickerView](https://github.com/Bigkoo/Android-PickerView)��[AndroidPicker](https://github.com/gzu-liyujiang/AndroidPicker)�޸����ϵ�,��Ҫ�ṩ�����л���ͬģʽ��view��
ͬʱҲ�Ż��˲��ִ�����������⣬����Ҳ����������ģʽ���л���

# ��װ
��app����Sample����android-pickers����library ����WheelPicker��SinglePicker��DatePicker��TimePicker��LinkagePicker��AddressPicker��NumberPicker��CarNumberPicker�ȡ�
#### demo����
[����](http://opmkud60m.bkt.clouddn.com/app-release.apk)
#### Զ�̼���JitPack��
����[![](https://jitpack.io/v/addappcn/android-pickers.svg)](https://jitpack.io/#addappcn/android-pickers)�Ĳֿ⣺
��һ��������Ŀ��Ŀ¼�µ�build.gradle��ӣ�
```
repositories {
    maven {
        url "https://www.jitpack.io"
    }
}
```
�ڶ���������Ŀ��appģ���µ�build.gradle��ӣ�
```
dependencies {
    compile 'com.github.addappcn:android-pickers:1.0.0'
}
```

# ProGuard
���ڵ�ַѡ����ʹ����[fastjson](https://github.com/alibaba/fastjson)������������ʱ����Ҫ�����������ƵĹ��򣬲�����Province��City��ʵ���ࡣ
```
-keepattributes InnerClasses,Signature
-keepattributes *Annotation*

-keep class cn.addapp.pickers.entity.** { *;}
```

# Sample �������÷����ʾ����Ŀ��
�̳��Զ�����չѡ������
```java
       CustomPicker picker = new CustomPicker(this);
               picker.setOffset(1);//��ʾ����Ŀ��ƫ����������Ϊ��offset*2+1��
               picker.setGravity(Gravity.CENTER);//����
               picker.setOnItemPickListener(new OnItemPickListener<String>() {
                   @Override
                   public void onItemPicked(int position, String option) {
                       showToast("index=" + position + ", item=" + option);
                   }
               });
               picker.show();
```
��Ƕ��ͼѡ������
```java
        final TextView textView = findView(R.id.wheelview_tips);
                WheelListView wheelListView = findView(R.id.wheelview_single);
                wheelListView.setItems(new String[]{"��������", "���ݴ�����", "����56����������֮��", "��57������"}, 1);
                wheelListView.setSelectedTextColor(0xFFFF00FF);
                LineConfig config = new LineConfig();
                config.setColor(Color.parseColor("#26A1B0"));//����ɫ
                config.setAlpha(100);//��͸����
                config.setRatio((float) (1.0 / 5.0));//�߱���
                config.setThick(ConvertUtils.toPx(this, 3));//�ߴ�
                config.setShadowVisible(false);
                wheelListView.setLineConfig(config);
                wheelListView.setOnWheelChangeListener(new WheelListView.OnWheelChangeListener() {
                    @Override
                    public void onItemSelected(boolean isUserScroll, int index, String item) {
                        textView.setText("index=" + index + ",item=" + item);
                    }
                });
                picker = new CarNumberPicker(this);
                picker.setWeightEnable(true);
                picker.setColumnWeight(0.5f,0.5f,1);
                picker.setWheelModeEnable(true);
                picker.setTextSize(18);
                picker.setSelectedTextColor(0xFF279BAA);//ǰ��λֵ��͸����
                picker.setUnSelectedTextColor(0xFF999999);
                picker.setCanLoop(true);
                picker.setOffset(3);
                picker.setOnMoreItemPickListener(new OnMoreItemPickListener<String>() {
                    @Override
                    public void onItemPicked(String s1, String s2, String s3) {
                        s3 = !TextUtils.isEmpty(s3) ? ",item3: "+s3 : "";
                        Toast.makeText(NextActivity.this, "item1: "+s1 +",item2: "+s2+ s3, Toast.LENGTH_SHORT).show();
                    }
                });
                picker.setOnMoreWheelListener(new OnMoreWheelListener() {
                    @Override
                    public void onFirstWheeled(int index, String item) {
                        textView.setText(item + ":" + picker.getSelectedSecondItem());
                    }
                    @Override
                    public void onSecondWheeled(int index, String item) {
                        textView.setText(picker.getSelectedFirstItem() + ":" + item);
                    }
                    @Override
                    public void onThirdWheeled(int index, String item) {
                    }
                } );
                ViewGroup viewGroup = findView(R.id.wheelview_container);
                viewGroup.addView(picker.getContentView());
```
ѡ�������������
```java
        boolean isChinese = Locale.getDefault().getDisplayLanguage().contains("����");
        OptionPicker picker = new OptionPicker(this,
                isChinese ? new String[]{
                        "ˮƿ", "˫��", "����", "��ţ", "˫��", "��з",
                        "ʨ��", "��Ů", "���", "��Ы", "����", "Ħ��"
                } : new String[]{
                        "Aquarius", "Pisces", "Aries", "Taurus", "Gemini", "Cancer",
                        "Leo", "Virgo", "Libra", "Scorpio", "Sagittarius", "Capricorn"
                });
        picker.setLabel(isChinese ? "��" : "");
        picker.setCycleDisable(true);//����ѭ��
        picker.setLineConfig(config);
        picker.setTopHeight(50);//�����������߶�
        picker.setTopLineColor(0xFF33B5E5);//�����������»�����ɫ
        picker.setTopLineHeight(1);//�����������»��߸߶�
        picker.setTitleText(isChinese ? "��ѡ��" : "Please pick");
        picker.setTitleTextColor(0xFF999999);//����������ɫ
        picker.setTitleTextSize(12);//�����������ִ�С
        picker.setCancelTextColor(0xFF33B5E5);//����ȡ����ť������ɫ
        picker.setCancelTextSize(14);
        picker.setSubmitTextColor(0xFF33B5E5);//����ȷ����ť������ɫ
        picker.setSubmitTextSize(14);
        picker.setTextColor(0xFFEE0000, 0xFF999999);//�м������������ɫ
        WheelView.LineConfig config = new WheelView.LineConfig();
        config.setColor(0xFFEE0000);//����ɫ
        config.setAlpha(140);//��͸����
        picker.setLineConfig(config);
        picker.setBackgroundColor(0xFFE1E1E1);
        //picker.setSelectedItem(isChinese ? "����" : "Sagittarius");
        picker.setSelectedIndex(10);//Ĭ��ѡ����
        picker.setOnOptionPickListener(new OptionPicker.OnOptionPickListener() {
            @Override
            public void onOptionPicked(int index, String item) {
                showToast("index=" + index + ", item=" + item);
            }
        });
        picker.show();
```

![Ч��ͼ](/screenshots/Screenshot_2017-04-21-15-45-59.png)
![Ч��ͼ](/screenshots/Screenshot_2017-04-21-15-46-11.png)
![Ч��ͼ](/screenshots/Screenshot_2017-04-21-15-56-00.png)
![Ч��ͼ](/screenshots/Screenshot_2017-04-21-15-56-22.png)
![Ч��ͼ](/screenshots/Screenshot_2017-04-21-15-56-38.png)
![Ч��ͼ](/screenshots/Screenshot_2017-04-21-15-56-50.png)

## License

    Copyright 2017 ����� (android-pickers)

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

