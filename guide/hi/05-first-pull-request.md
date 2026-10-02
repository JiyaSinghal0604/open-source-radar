5. आपका पहला Pull Request, चरण-दर-चरण

यह fork से लेकर Pull Request खोलने तक का पूरा workflow है। OWNER/REPO को project के नाम से और your-username को अपने GitHub username से बदलें।

English version

1. Fork और clone करें

Fork GitHub पर repository की आपकी अपनी copy होती है। आप अपने fork में push करते हैं और फिर मूल project (जिसे upstream कहा जाता है) से अपने changes को pull करने के लिए कहते हैं।

gh repo fork OWNER/REPO --clone
cd REPO
git remote -v
# origin    https://github.com/your-username/REPO.git  (your fork)
# upstream  https://github.com/OWNER/REPO.git          (the original)


GitHub CLI के बिना: repository page पर Fork पर click करें, फिर:

git clone https://github.com/your-username/REPO.git
cd REPO
git remote add upstream https://github.com/OWNER/REPO.git


बड़ी repository है? git clone --filter=blob:none URL केवल ज़रूरत पड़ने पर file contents download करता है, जिससे cloning बहुत तेज़ हो जाती है।

2. एक branch बनाएँ

अपने fork की default branch पर कभी काम न करें। हर change की शुरुआत latest upstream code से करें:

git fetch upstream
git switch -c fix-empty-username upstream/main   # use the project's default branch name


Branch का नाम change के अनुसार रखें, जैसे fix-empty-username या docs-install-windows।

3. कुछ बदलने से पहले इसे build करें और tests चलाएँ

Project की CONTRIBUTING.md या DEVELOPMENT.md का पालन करें। language quickstarts सामान्य commands दिखाते हैं। Unmodified code पर पहले tests चलाएँ:

अगर वे pass होते हैं, तो आपके पास एक working baseline है।

अगर कुछ tests पहले से fail हो रहे हैं, तो ध्यान दें कि कौन-से tests fail हो रहे हैं। वे failures आपकी वजह से नहीं हैं, और अगर relevant हों तो आपको अपने PR में उनका उल्लेख करना चाहिए।

4. समस्या को reproduce करें

Fix करने से पहले, issue में दिए गए steps का उपयोग करके अपनी machine पर साबित करें कि bug मौजूद है। लिखें कि क्या होता है और इसके बजाय क्या होना चाहिए। अगर आप इसे reproduce नहीं कर सकते, तो अनुमान लगाकर fix करने के बजाय issue पर अपनी version और environment के साथ यह बात बताएँ।

5. एक failing test लिखें

जिस code को आप बदल रहे हैं उसकी test file खोजें और ऐसा test जोड़ें जो bug को दिखाए। उसे चलाएँ और उसे fail होते हुए देखें। इससे आपको और reviewer को पता चलता है कि आपका test वास्तव में bug को cover करता है।

हर change के लिए test ज़रूरी नहीं होता (उदाहरण के लिए documentation fixes), लेकिन bug fixes के लिए लगभग हमेशा test होना चाहिए। कई projects बिना test के fix को merge नहीं करेंगे।

6. समस्या को ठीक करने वाला सबसे छोटा change करें

केवल वही बदलें जिसकी issue के लिए आवश्यकता है। अचानक किए गए refactors, renames या unrelated code की reformatting न करें: इससे आपके Pull Request का review करना कठिन हो जाता है।

आसपास के code की style का पालन करें, भले ही आप इसे अलग तरीके से लिखना पसंद करते हों।

Step 5 वाला test फिर से चलाएँ। अब उसे pass होना चाहिए।

7. सभी checks local रूप से चलाएँ

कम से कम उस हिस्से के लिए project का CI जो चलाता है, वही checks चलाएँ जिसे आपने बदला है:

test suite (या उसका relevant हिस्सा)

formatter (जैसे prettier, black/ruff format, cargo fmt, gofmt)

linter (जैसे eslint, ruff, clippy, go vet)

अगर project इसका उपयोग करता है तो type checking (tsc, mypy)

कुछ projects changelog entry या "changeset" file भी चाहते हैं। Contributing guide में इसका उल्लेख होगा।

8. Commit करें
git add path/to/changed/files
git commit


एक स्पष्ट message लिखें। Project की convention का पालन करें (git log --oneline -20 देखें)। एक सामान्य रूप कुछ ऐसा होता है:

parser: handle empty username in login prompt

An empty username made the prompt loop forever because validation
rejected it without telling the user. Show the validation error and
ask again instead.

Fixes #1234


पहली line: छोटा summary, अक्सर area के नाम से शुरू होता है या fix: या docs: जैसे Conventional Commits
 type से।

Body: क्या गलत था और यह change उसे क्यों ठीक करता है।

Fixes #1234 PR merge होने पर issue को अपने-आप बंद कर देता है।

अगर project को DCO sign-off की आवश्यकता है, तो git commit -s का उपयोग करें (chapter 6 देखें)।

9. Push करें और Pull Request खोलें
git push -u origin fix-empty-username
gh pr create --repo OWNER/REPO --fill   # or open the link git prints, in your browser


अगर project में Pull Request template है, तो उसे भरें। Chapter 7 में अच्छी description कैसी होनी चाहिए, इसके बारे में बताया गया है। संक्षेप में: क्या गलत था, आपने क्या बदला, आपने इसे कैसे test किया और यह किस issue को fix करता है।

10. अपनी branch को up to date रखें

अगर आपका PR merge होने से पहले upstream branch में changes आ जाते हैं और conflicts होते हैं, तो अपनी branch को update करें:

git fetch upstream
git rebase upstream/main
# fix any conflicts, then: git add <files> && git rebase --continue
git push --force-with-lease


--force-with-lease उस branch को update करने का सुरक्षित तरीका है जिसे आपने rewrite किया है; यह उन commits को overwrite करने से मना करता है जो आपके पास local रूप से मौजूद नहीं हैं। कुछ projects आपकी branch में upstream/main को merge करना पसंद करते हैं, rebasing नहीं; उनके guide का पालन करें।

Checklist

 Branch latest upstream default branch से बनाई गई है।

 मेरे change से पहले tests pass हुए (या मैंने existing failures को note किया)।

 मैंने bug को reproduce किया और ऐसा test लिखा जो fix से पहले fail हुआ।

 Diff में केवल इस issue के लिए आवश्यक changes हैं।

 Tests, formatter और linter local रूप से pass होते हैं।

 Commit message project की convention का पालन करता है और issue को reference करता है।

 PR template भरा गया है।

अगला: शुरू करने से पहले जाँचने वाले नियम