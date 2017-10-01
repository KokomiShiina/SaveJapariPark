# notatsukinotanoshi
No tatsuki No Tanoshi!

# Specifications
Framework `.NET Core 2.1.1 MVC`  
Scripts
```
PHP 7.0
ASP.NET MVC 4
```

# Git flow
`master` 已經被鎖定，所有操作必須根據流程進行。  


## Branching
新功能：`feature/名稱`  
修正：`hotfix/名稱`  
發怖：`release/版本`  

## Flow
### Before Started
進行修改前，請根據上述`branch`命名方產生新`branch`並`checkout`，避免失去工作進度。

### Updating master
1. 完成工作以後，必須在GitHub網頁上發怖新[Pull Request (PR)](https://github.com/tnsogs02/notatsukinotanoshi/pulls)，並請求最少一人過目。  
檢查並不需要細閱代碼，但是必須確保沒有未被修正的Merge conflict，以下是一個Merge conflict的例子，這個將會造成系統運行失敗，所以必須留意。 `HEAD`下方的內容是目前repo的代碼，`branch`上方則是你的代碼，請自行斟酌要使用哪一段，或者適當地合拼代碼。
```
<<<<<<< HEAD
open an issue
=======
ask your question in IRC.
>>>>>>> branch-a
```

2. 修正所有Merge conflict後，reviewer可以在PR頁面的右上方選`Review Pull Request`，輸入內容後Approve，PR就此完成。
3. 最後，如果系統沒有顯示Merge conflict，就可以直接進行`merge`。Review後不必馬上進行merge，可以在此進行改進，直至滿意。
4. 完成Merge後，請順便Delete branch，以防止冗餘數據積蓄。

# Application structure
基本部分採用Model-View-Control (MVC)設計，透過Controller控制網頁內容。
以上三個部分分別在`Controllers`，`Models`，`Views`資料夾。  
網頁的顯示方式為: `http://notatsukinotanoshi.tw/{Controllers}/{Actions}`

## Controllers
Controllers主要負責網頁顯示方式，必須以 `{Name}Controller.cs` 命名。
裡面的 `IAction` method為可定義Action。

以下代碼為例子
```csharp
namespace notatsukinotanoshi.Controllers
{
    public class HomeController : Controller
    {
        public IActionResult Index()
        {
            return View();
        }
    }
}
```
如瀏覽網頁 `http://notatsukinotanoshi.tw/Home/Index/`，將會直接顯示相對應的View。  

## Views
Views為主要顯示內容，主要以HTML編寫，`Razor Template`僅提供輔助功能，例如可以由`Controller`先進行運算，再將內容加入到顯示頁面。  
View的位置必須根據Controller設置，並放置於`Views`資料夾內。  
`Razor Template`支援的命名方式包括`Views/Home.Index.cshtml`（無資料夾）或者`Views/Home/Index.cshtml`  
* 注意：`Views.Home.Index.cshtml` 並不包括在內。

### Shared Views
`Views/Shared`內的檔案為共享內容，`_Layout.cshtml`為每個網頁必顯示的內容，一般`View/Action.cshtml`僅為Content部分，故不用加入header/footer。  
`_Layout.cshtml` 內的 `@RenderBody()` 為Content出現的部分。

### Environment Tag
Template內有數個`Enviroment`的Tag存在，將會根據App的環境控制出現的檔案。  
`<environment include="Development">`：僅在開發環境出現  
`<environment exclude="Development">`：在非開放環境出現（staging/production）  

## Resouce
本系統已經設置Localization，語言資料放置於`Resources`資料夾內，受於系統限制，語言資料必須根據相對應的 Controller/View/Model 命名。  
例如首頁的語言資料為 `Views/Home/Index.{local}.resx`

目前支援的語言包括
```
en: 英文
zh: 中文
ja: 日文
ko: 韓文
```

# Usage
### Helper classes
`bundleconfig.json`: 負責產生並minify代碼

## Authors
* [ Place Holder ]
* [ Place Holder ]
* [ Place Holder ]
* Sakura - Initial Work - [lamyauping](https://github.com/lamyauping)

## License
Refer to license
