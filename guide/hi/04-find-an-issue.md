4. ऐसा issue खोजें जिसे आप पूरा कर सकें

एक अच्छा पहला issue छोटा, स्पष्ट रूप से बताया गया, दोबारा reproduce किया जा सकने वाला और किसी अन्य व्यक्ति द्वारा पहले से किया जा रहा नहीं होना चाहिए। आखिरी बात वह जगह है जहाँ ज़्यादातर नए contributors का समय बर्बाद होता है।

English version

कहाँ देखें

इस repository का issue index और website
: newcomers के लिए labeled खुले issues, जिन्हें पहले से किसी assignee या linked open pull request वाले issues को हटाने के लिए filter किया गया है।

प्रोजेक्ट का अपना issue tracker, जिसे उसके newcomer labels के अनुसार filter किया गया हो।

GitHub search, उदाहरण के लिए:

is:issue is:open no:assignee -linked:pr label:"good first issue" language:python


no:assignee assigned issues को छिपाता है और -linked:pr उन issues को छिपाता है जिनसे पहले से कोई pull request जुड़ा हुआ है। पुराने issues को छोड़ने के लिए updated:>2026-06-01 जोड़ें (हाल की तारीख का उपयोग करें)।

आपको कौन-से labels दिखाई देंगे
Label	आम तौर पर इसका मतलब
good first issue, first-timers-only, beginner, E-easy	Maintainers को लगता है कि कोई newcomer इसे कर सकता है, अक्सर guidance के साथ
help wanted, PR welcome, up-for-grabs	Maintainers चाहते हैं कि कोई दूसरा व्यक्ति इसे करे; यह हमेशा छोटा काम नहीं होता
bug, confirmed, has: repro	एक वास्तविक defect; confirmed का मतलब है कि किसी maintainer ने इसे reproduce किया है
needs-triage, needs-info, question	अभी तैयार नहीं: समस्या अभी तक समझी नहीं गई है
design, rfc, discussion, blocked	Pull request के लिए अभी तैयार नहीं; किसी निर्णय का इंतज़ार है

हर project अपने labels खुद तय करता है। प्रोजेक्ट के Issues → Labels पेज पर labels के descriptions देखें।

क्या कोई और पहले से इस पर काम कर रहा है?

Code की एक भी line लिखने से पहले इन सभी चीज़ों को जाँचें:

Assignees. अगर किसी व्यक्ति को assign किया गया है, तो issue पहले ही लिया जा चुका है।

Linked pull requests. Right sidebar ("Development") और timeline में "linked a pull request" या PRs से जुड़े "mentioned this issue" events देखें। एक open PR का मतलब है कि issue लिया जा चुका है; एक बंद और unmerged PR का मतलब हो सकता है कि approach को reject कर दिया गया था, इसलिए कारण पढ़ें।

Comments. "I'd like to work on this" या "working on it" जैसे comments देखें। अगर claim हाल का है (कुछ हफ्ते पहले का) और उस व्यक्ति ने बातचीत बंद नहीं की है, तो कोई दूसरा issue चुनें।

Open pull requests खोजें और issue number या title के keywords देखें। हर PR issue से सही तरीके से link नहीं होती।

अगर कोई claim पुराना है और वह व्यक्ति चुप हो गया है, तो विनम्रता से पूछना आम तौर पर ठीक है: "Hi @name, are you still working on this? If not, I'd be happy to pick it up." फिर कुछ दिनों तक इंतज़ार करें।

क्या आप इसे पूरा कर सकते हैं?

ईमानदारी से अनुमान लगाएँ। आपके लिए एक अच्छा पहला issue:

उसका expected behaviour स्पष्ट हो। आप एक वाक्य में बता सकें कि इसके बजाय क्या होना चाहिए।

उसे reproduce किया जा सके। Issue में steps, snippet या failing command हो। अगर नहीं है, तो उसे reproduce करना आपका पहला काम है, और reproduction को post करना भी अपने-आप में एक contribution है।

वह local हो। आप अनुमान लगा सकें कि कौन-सी file या function शामिल है। Issue में बताए गए error message या function name के लिए codebase में search करें।

उसमें design decision की आवश्यकता न हो। अगर maintainers अभी भी इस बात पर चर्चा कर रहे हैं कि यह कैसे काम करना चाहिए, तो इंतज़ार करें।

वह आपकी machine पर चलता हो। अगर आप macOS पर हैं तो Windows-only bugs से बचें, GPU के बिना GPU bugs से बचें, आदि।

किसी issue का आकार जल्दी समझने का तरीका

Issue को लेने से पहले 20 से 30 मिनट बिताएँ:

Project को clone करें और एक बार उसकी test suite चलाएँ (chapter 5)।

Bug को reproduce करें, या feature के लिए code में सही जगह खोजें।

उस हिस्से की मौजूदा test file खोजें।

अगर आप तीनों काम कर पाए, तो issue शायद सही आकार का है। अगर 30 मिनट बाद भी आप उलझे हुए हैं, तो कोई दूसरा issue आज़माएँ, या issue पर कोई specific question पूछें (chapter 7)।

Checklist

 कोई assignee नहीं है, कोई linked open PR नहीं है और comments में कोई recent claim नहीं है।

 मैं expected behaviour को एक वाक्य में बता सकता/सकती हूँ।

 मैंने समस्या को reproduce किया है, या मुझे ठीक-ठीक पता है कि change कहाँ करना है।

 Maintainers अभी भी approach पर बहस नहीं कर रहे हैं।

अगला: आपका पहला Pull Request, चरण-दर-चरण