# Superstore Sales Analysis - Power BI Project

ဒီပရောဂျက်ကတော့ Superstore ရောင်းအားဒေတာတွေကို Power BI နဲ့ ပေါ့ပေါ့ပါးပါး သန့်ရှင်းရေးလုပ်ပြီး ဘယ်လိုခွဲခြမ်းစိတ်ဖြာလဲဆိုတာ ပြထားတာပါ။
### **ဒီဒေတာလေးတွေ ဘယ်ကရလဲ? (Where did I get this data from?)**

ဒီပရောဂျက်မှာ သုံးထားတဲ့ "Sample - Superstore.csv" ဒေတာတွေကတော့ Data Analysis ပရောဂျက်တွေအတွက် အမြဲလိုလို သုံးနေကျ နမူနာဒေတာလေးတွေပါ။ 
ဒီကနေ ဒေါင်းလို့ရပါတယ်နော်:
(https://www.kaggle.com/datasets/ishanshrivastava28/superstore-sales)
* **Kaggle မှာ ရှာမယ်ဆိုရင်လည်း "Sample Superstore" လို့ ရိုက်ရှာကြည့်လို့ရပါတယ်။**

---

### **ဒေတာလေးတွေ သန့်ရှင်းရေးလုပ်နည်း (Data Cleaning Fun!)**

Power Query Editor မှာ အောက်ပါအတိုင်း ရှင်းထုတ်ခဲ့တာလေးတွေပါ။

* **အဆင့် ၁: ခေါင်းစဉ်လေးတွေ နေရာချမယ် (Promote Headers)**
    * ပထမဆုံးတန်းက စာလုံးလေးတွေက တကယ်တမ်းကျတော့ column နာမည်တွေဖြစ်နေလို့ သူတို့ကို ခေါင်းစဉ်အဖြစ် ပြောင်းလိုက်တယ်။ (Home > Use First Row as Headers)

* **အဆင့် ၂: ဒေတာအမျိုးအစားလေးတွေ ပြင်မယ် (Fix Data Types)**
    * **`Order Date`** နဲ့ **`Ship Date`** ကို **Date** ပုံစံလေးတွေ ဖြစ်အောင် ပြောင်းခဲ့တယ်။ (Locale `en-US` နဲ့ ဖတ်တာ ပိုအဆင်ပြေတယ်)
    * **`Sales`**၊ **`Discount`**၊ **`Profit`** တွေကတော့ ပိုက်ဆံတွေဆိုတော့ **Decimal Number** အဖြစ် ပြောင်းလိုက်တယ်။
    * **`Quantity`** ကတော့ ပစ္စည်းအရေအတွက်ဆိုတော့ **Whole Number** ပေါ့။
    * **`Postal Code`** က ဂဏန်းတွေဖြစ်ပေမယ့် ပေါင်းစရာမလိုတော့ **Text** အဖြစ် ပြောင်းထားတာ ပိုစိတ်ချရတယ်။
    * ကျန်တဲ့ column အများစုကတော့ **Text** တွေပါပဲ။

* **အဆင့် ၃: ပျောက်နေတဲ့ ဒေတာလေးတွေ ရှင်းမယ် (Handle Missing Values)**
    * **`Postal Code`** မှာ ပျောက်နေတဲ့ `null` လေးတွေ ရှိလို့ `"N/A"` လို့ ပြောင်းလိုက်တယ်။ (Transform > Replace Values)
    * တခြားနေရာတွေမှာ ပျောက်တာတွေ ရှိမရှိလည်း အပေါ်ယံလေး လိုက်စစ်ကြည့်ခဲ့တယ်။

* **အဆင့် ၄: ထပ်နေတဲ့ ဒေတာလေးတွေ ဖယ်ထုတ်မယ် (Remove Duplicates)**
    * **`Row ID`** column ကို ရွေးပြီး ထပ်နေတဲ့ တန်ဖိုးတွေ ရှိခဲ့ရင် ဖယ်ပစ်လိုက်တယ်။ (Right-click > Remove Duplicates) (ဒီဒေတာမှာတော့ ထပ်နေတာ ရှားပါတယ်)

* **အဆင့် ၅: စာသားလေးတွေ သန့်ရှင်းမယ် (Clean Text Data)**
    * `Category`, `Sub-Category`, `Segment`, `Ship Mode`, `Country`, `Region`, `City`, `State` လိုမျိုး စာသား column တွေကို ရွေးပြီး-
    * အစ/အဆုံးမှာ မလိုတဲ့ နေရာလွတ်တွေကို ရှင်းပစ်ခဲ့တယ်။ (Transform > Format > Trim)
    * စာလုံးတိုင်းရဲ့ ပထမဆုံး စာလုံးလေးတွေကို စာလုံးအကြီး ဖြစ်အောင် ပြောင်းလိုက်တယ်။ (ဥပမာ: "office supplies" ကနေ "Office Supplies" ဖြစ်သွားတာပေါ့) (Transform > Format > Proper Case)

* **အဆင့် ၆: မလိုတာတွေ ဖယ်ထုတ်မယ် (Filter Out Invalid/Irrelevant Data)**
    * **`Quantity`** နဲ့ **`Sales`** တွေမှာ `0` ဒါမှမဟုတ် အနှုတ်တန်ဖိုးတွေ ရှိနိုင်လို့ အဲဒါတွေကို ဖယ်ထုတ်ပစ်ခဲ့တယ်။ (Filter > Number Filters > Greater Than... > 0) (အနှုတ်တန်ဖိုးတွေက ပြန်အမ်းတာတွေ ဖြစ်နိုင်တယ်၊ ဒါပေမယ့် ဒီ Analysis အတွက် အပေါင်းတန်ဖိုးတွေကိုပဲ ကြည့်ချင်လို့ပါ)

* **အဆင့် ၇: ကိုယ်ပိုင် Column လေးတွေ ထပ်ထည့်မယ် (Add Custom Columns)**
    * **`Sales Per Unit`** ဆိုတဲ့ column အသစ်ကို `[Sales] / [Quantity]` နဲ့ တွက်ပြီး Decimal Number အဖြစ် ပြောင်းလိုက်တယ်။
    * **`Profit Margin (%)`** ဆိုတာလေးကိုတော့ `[Profit] / [Sales]` နဲ့ တွက်ပြီး Decimal Number အဖြစ် ပြောင်းခဲ့တယ်။
    * `Order Date` ကနေ **`Order Year`**၊ **`Order Month`**၊ **`Order Day`** ဆိုပြီး သီးသန့် column လေးတွေ ခွဲထုတ်ခဲ့တယ်။ (Add Column > Date > Year/Month/Day)
    * စိတ်ဝင်စားရင် **`Order Day Name`** (ဥပမာ: Monday, Tuesday) ကိုလည်း ထုတ်ခဲ့တယ်။ (Add Column > Date > Day > Name of Day)

---

### **Power BI Report ထဲက Visual လေးတွေ (Power BI Report Visualizations)**

ဒေတာတွေ သန့်ရှင်းပြီး အသင့်ဖြစ်ပြီဆိုတော့ Power BI Report ထဲမှာ ဒီလို Visual လေးတွေကို ဖန်တီးခဲ့တယ်-

* **စုစုပေါင်း ရောင်းအား (Total Sales)**
* **အလုံးစုံ အမြတ်ရာခိုင်နှုန်း (Overall Profit Margin %)**
* **နှစ်အလိုက် ရောင်းအား ခေတ်ရေစီးကြောင်း (Sales Trend Over Time)**
* **Category အလိုက် ရောင်းအား (Sales by Category)**
* **Sub-Category အလိုက် အမြတ် (Profit by Sub-Category)**
