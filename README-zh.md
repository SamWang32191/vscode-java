# Visual Studio Code 的 Java™ 語言支援

[![Visual Studio Marketplace](https://img.shields.io/visual-studio-marketplace/v/redhat.java?style=for-the-badge&label=VS%20Marketplace&logo=visual-studio-code)](https://marketplace.visualstudio.com/items?itemName=redhat.java)
[![Installs](https://img.shields.io/visual-studio-marketplace/i/redhat.java?style=for-the-badge)](https://marketplace.visualstudio.com/items?itemName=redhat.java)
[![在 Gitter 上加入聊天 https://gitter.im/redhat-developer/vscode-java](https://img.shields.io/gitter/room/redhat-developer/vscode-java?style=for-the-badge&logo=gitter)](https://gitter.im/redhat-developer/vscode-java)
[![Build Status](https://img.shields.io/github/actions/workflow/status/redhat-developer/vscode-java/pr-verify.yml?branch=main&style=for-the-badge&logo=github)](https://github.com/redhat-developer/vscode-java/actions?query=workflow:pr-verify)
[![License](https://img.shields.io/github/license/redhat-developer/vscode-java?style=for-the-badge&logo=eclipse)](https://github.com/redhat-developer/vscode-java/blob/main/LICENSE)

透過 [Eclipse™ JDT Language Server](https://github.com/eclipse/eclipse.jdt.ls) 提供 Java™ 語言支援，其利用了 [Eclipse™ JDT](http://www.eclipse.org/jdt/)、[M2Eclipse](http://www.eclipse.org/m2e/) 和 [Buildship](https://github.com/eclipse/buildship)。

快速入門
============
1. 安裝此擴充套件
2. 在以下平台上，擴充套件應無需任何設定即可啟動：`win32-x64`、`darwin-x64`、`darwin-arm64`、`linux-x64`、`linux-arm64`。
若在其他平台或使用「通用」版本，您可以[設定](#設定-jdk)一個 _Java_ 開發工具包。它必須是 Java 21 或更高版本。
3. （可選）為您的專案下載並安裝一個 Java 開發工具包（支援 Java 1.8 或更高版本）。詳情請參閱 [專案 JDKs](#專案-jdks)
4. 當您首次存取 Java 檔案時，擴充套件會被啟動
    * 能辨識目錄階層中帶有 *Maven* 或 *Gradle* 建置檔案的專案。

功能
=========
![ screencast ](https://raw.githubusercontent.com/redhat-developer/vscode-java/main/images/vscode-java.0.0.1.gif)

* 支援從 Java 1.8 到 Java 25 的程式碼
* Maven pom.xml 專案支援
* Gradle 專案支援（實驗性支援 Android 專案匯入）
* 獨立 Java 檔案支援
* 輸入時即時回報解析與編譯錯誤
* 程式碼補完
* 程式碼/原始碼操作 / 重構
* Javadoc 懸浮提示
* 整理 imports
	- 手動觸發或儲存時觸發
	- 使用 `Ctrl+Shift+v`（Mac 上為 `Cmd+Shift+v`）將程式碼貼上到 java 檔案時。
* 類型搜尋
* 程式碼大綱
* 程式碼摺疊
* 程式碼導覽
* Code lens（參考/實作）
* 語法高亮
* 程式碼格式化（輸入時/選取時/檔案）
* 程式碼片段
* 註釋處理支援（Maven 專案自動處理）
* 語意選取
* 診斷標籤
* 呼叫階層
* 類型階層
* 內嵌提示

若要啟動和偵錯您的 Java 程式，建議您安裝 *[Java Debug Extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug)*。

請參閱 [changelog](CHANGELOG.md) 以了解最新版本。您也可以在專案 [Wiki](https://github.com/redhat-developer/vscode-java/wiki) 中找到有用的資訊。

設定 JDK
===============
## Java 工具 JDK
現在 Java 擴充套件將發布特定平台的版本，它將為支援的平台（如 `win32-x64`、`linux-x64`、`linux-arm64`、`darwin-x64`、`darwin-arm64`）內嵌一個 JRE。內嵌的 JRE 用於啟動 Java 語言伺服器。使用者只需負責設定 [專案 JDKs](#專案-jdks) 來編譯您的 Java 專案。

以下部分僅為沒有內嵌 JRE 的通用版本保留。

>工具 JDK 將用於啟動 Java 語言伺服器。預設情況下，它也將用於編譯您的專案。Java 21 是最低要求的版本。\
>
>Java 開發工具包的路徑可以透過 VS Code 設定（工作區/使用者設定）中的 `java.jdt.ls.java.home` 指定。如果未指定，它將按以下順序搜尋，直到找到符合當前最低要求的 JDK。
> - `JDK_HOME` 環境變數
> - `JAVA_HOME` 環境變數
> - 當前的系統路徑

## 專案 JDKs
如果您需要針對不同的 JDK 版本編譯您的專案，建議您在使用者設定中設定 `java.configuration.runtimes` 屬性，例如：

```json
"java.configuration.runtimes": [
  {
    "name": "JavaSE-1.8",
    "path": "/path/to/jdk-8",
  },
  {
    "name": "JavaSE-11",
    "path": "/path/to/jdk-11",
  },
  {
    "name": "JavaSE-25",
    "path": "/path/to/jdk-25",
    "default": true
  },
]
```
當您開啟獨立的 Java 檔案時，將使用預設的執行環境。

可用指令
==========================
提供以下指令：
- `切換到標準模式 (Switch to Standard Mode)`：將 Java 語言伺服器切換到 `Standard` 模式。此指令僅在 Java 語言伺服器處於 `LightWeight` 模式時可用。
- `Java: 重新載入專案 (Reload Projects)` (`Shift+Alt+U`)：根據專案建置描述檔，強制更新專案設定/類別路徑（例如，相依性變更或 Java 編譯層級）。
- `Java: 將 Java 專案匯入工作區 (Import Java Projects into Workspace)`：偵測並將所有 Java 專案匯入 Java 語言伺服器工作區。
- `Java: 開啟 Java 語言伺服器日誌檔案 (Open Java Language Server Log File)`：開啟 Java 語言伺服器日誌檔案，有助於疑難排解。
- `Java: 開啟 Java 擴充套件日誌檔案 (Open Java Extension Log File)`：開啟 Java 擴充套件日誌檔案，有助於疑難排解。
- `Java: 開啟所有日誌檔案 (Open All Log Files)`：同時開啟 Java 語言伺服器日誌檔案和 Java 擴充套件日誌檔案。
- `Java: 強制 Java 編譯 (Force Java Compilation)` (`Shift+Alt+B`)：手動觸發工作區的編譯。
- `Java: 重建專案 (Rebuild Projects)`：手動觸發所選專案的完整建置。
- `Java: 開啟 Java 格式化程式設定 (Open Java Formatter Settings)`：開啟 Eclipse 格式化程式設定。如果不存在，則建立一個新的設定檔案。
- `Java: 清理 Java 語言伺服器工作區 (Clean Java Language Server Workspace)`：清理 Java 語言伺服器工作區。
- `Java: 附加原始碼 (Attach Source)`：將 jar/zip 原始碼附加到目前開啟的二進位類別檔案。此指令僅在編輯器右鍵選單中可用。
- `Java: 將資料夾新增到 Java 原始碼路徑 (Add Folder to Java Source Path)`：將所選資料夾新增到其專案原始碼路徑。此指令僅在檔案總管右鍵選單中可用，且僅適用於非受控資料夾。
- `Java: 從 Java 原始碼路徑移除資料夾 (Remove Folder from Java Source Path)`：從其專案原始碼路徑移除所選資料夾。此指令僅在檔案總管右鍵選單中可用，且僅適用於非受控資料夾。
- `Java: 列出所有 Java 原始碼路徑 (List All Java Source Paths)`：列出 Java 語言伺服器工作區所辨識的所有 Java 原始碼路徑。
- `Java: 顯示建置工作狀態 (Show Build Job Status)`：在 Visual Studio Code 終端機中顯示 Java 語言伺服器的工作狀態。
- `Java: 前往超級實作 (Go to Super Implementation)`：前往編輯器中目前選定符號的超級實作。
- `Java: 重新啟動 Java 語言伺服器 (Restart Java Language Server)`：重新啟動 Java 語言伺服器。

支援的 VS Code 設定
==========================
支援以下設定：

* `java.home`：**已棄用，請改用 'java.jdt.ls.java.home'。** 用於啟動 Java 語言伺服器的 JDK 主資料夾絕對路徑。需要重新啟動 VS Code。
* `java.jdt.ls.lombokSupport.enabled`：是否啟用 lombok 支援。預設為 `true`。
* `java.jdt.ls.vmargs`：用於啟動 Java 語言伺服器的額外 VM 參數。需要重新啟動 VS Code。
* `java.errors.incompleteClasspath.severity`：指定當 Java 檔案的類別路徑不完整時訊息的嚴重性。支援的值為 `ignore`、`info`、`warning`、`error`。
* `java.trace.server`：追蹤 VS Code 與 Java 語言伺服器之間的通訊。
* `java.configuration.updateBuildConfiguration`：指定建置檔案的修改如何更新 Java 類別路徑/設定。支援的值為 `disabled`（不執行任何操作）、`interactive`（每次修改時詢問是否更新）、`automatic`（自動觸發更新）。
* `java.configuration.maven.userSettings`：Maven 的 user settings.xml 路徑。
* `java.configuration.checkProjectSettingsExclusions`：**已棄用，請使用 'java.import.generatesMetadataFilesAtProjectRoot' 來控制是否在專案根目錄產生專案中繼資料檔案。並使用 'files.exclude' 來控制是否從檔案總管中隱藏專案中繼資料檔案。** 控制是否從檔案總管中排除擴充套件產生的專案設定檔案（`.project`、`.classpath`、`.factorypath`、`.settings/`）。預設為 `false`。
* `java.referencesCodeLens.enabled`：啟用/停用參考的 code lenses。
* `java.implementationCodeLens`：為提供的類別啟用/停用實作的 code lens。
* `java.signatureHelp.enabled`：啟用/停用簽章輔助支援（在 `(` 上觸發）。
* `java.signatureHelp.description.enabled`：啟用/停用在簽章輔助中顯示描述。預設為 `false`。
* `java.contentProvider.preferred`：偏好的內容提供者（請參閱 [vscode-java-decompiler](https://github.com/dgileadi/vscode-java-decompiler) 中可用的第三方反編譯器）。
* `java.import.exclusions`：透過 glob 模式從匯入中排除資料夾。使用 `!` 來否定模式以允許子資料夾匯入。您必須包含父目錄。順序很重要。
* `java.import.gradle.enabled`：啟用/停用 Gradle 匯入器。
指定 Java 擴充套件使用的 Gradle 包裝器：
  * `java.import.gradle.wrapper.enabled`：從 'gradle-wrapper.properties' 檔案使用 Gradle。預設為 `true`。
  * `java.import.gradle.version`：如果 Gradle 包裝器遺失或停用，則使用特定版本的 Gradle。
  * `java.import.gradle.home`：如果 Gradle 包裝器遺失或停用且未指定 'java.import.gradle.version'，則從指定的本機安裝目錄或 GRADLE_HOME 使用 Gradle。
* `java.import.gradle.arguments`：傳遞給 Gradle 的參數。
* `java.import.gradle.jvmArguments`：傳遞給 Gradle 的 JVM 參數。
* `java.import.gradle.user.home`：GRADLE_USER_HOME 的設定。
* `java.import.gradle.offline.enabled`：啟用/停用 Gradle 離線模式。預設為 `false`。
* `java.import.maven.enabled`：啟用/停用 Maven 匯入器。
* `java.autobuild.enabled`：啟用/停用「自動建置」。
* `java.maxConcurrentBuilds`：設定同時進行的專案建置最大數量。
* `java.completion.enabled`：啟用/停用程式碼補完支援。
* `java.completion.guessMethodArguments`：指定在補完期間如何填寫參數。預設為 `auto`。
  - `auto`：僅在使用 Visual Studio Code - Insiders 時使用 `off`，其他平台預設為 `insertBestGuessedArguments`。
  - `off`：在補完期間不會插入方法參數。
  - `insertParameterNames`：在補完期間將插入參數名稱。
  - `insertBestGuessedArguments`：將根據程式碼上下文在補完期間插入最匹配的參數。
* `java.completion.filteredTypes`：定義類型過濾器。所有其完整限定名稱符合所選過濾器字串的類型將在內容輔助或快速修復建議中以及在整理匯入時被忽略。例如，'java.awt.*' 將隱藏 awt 套件中的所有類型。
* `java.completion.favoriteStaticMembers`：定義靜態成員或具有靜態成員的類型列表。
* `java.completion.importOrder`：定義匯入陳述式的排序順序。
* `java.format.enabled`：啟用/停用預設的 Java 格式化程式。
* `java.format.settings.url`：指定 [Eclipse 格式化程式 xml 設定](https://github.com/redhat-developer/vscode-java/wiki/Formatter-settings) 的 url 或檔案路徑。
* `java.format.settings.profile`：來自 Eclipse 格式化程式設定的選用格式化程式設定檔名稱。
* `java.format.comments.enabled`：在程式碼格式化期間包含註解。
* `java.format.onType.enabled`：啟用/停用輸入時格式化（在 `;`、`}` 或 `<return>` 上觸發）。
* `java.foldingRange.enabled`：啟用/停用智慧摺疊範圍支援。如果停用，它將使用 VS Code 提供的預設基於縮排的摺疊範圍。
* `java.maven.downloadSources`：在匯入 Maven 專案時，啟用/停用下載 Maven 原始碼成品。
* `java.maven.updateSnapshots`：強制更新 Snapshots/Releases。預設為 `false`。
* `java.codeGeneration.hashCodeEquals.useInstanceof`：在產生 hashCode 和 equals 方法時，使用 'instanceof' 來比較類型。預設為 `false`。
* `java.codeGeneration.hashCodeEquals.useJava7Objects`：在產生 hashCode 和 equals 方法時，使用 Objects.hash 和 Objects.equals。此設定僅適用於 Java 7 及更高版本。預設為 `false`。
* `java.codeGeneration.useBlocks`：在產生方法時，在 'if' 陳述式中使用區塊。預設為 `false`。
* `java.codeGeneration.generateComments`：在產生方法時產生方法註解。預設為 `false`。
* `java.codeGeneration.toString.template`：產生 toString 方法的範本。預設為 `${object.className} [${member.name()}=${member.value}, ${otherMembers}]`。
* `java.codeGeneration.toString.codeStyle`：產生 toString 方法的程式碼樣式。預設為 `STRING_CONCATENATION`。
* `java.codeGeneration.toString.skipNullValues`：產生 toString 方法時跳過 null 值。預設為 `false`。
* `java.codeGeneration.toString.listArrayContents`：列出陣列的內容，而不是使用原生的 toString()。預設為 `true`。
* `java.codeGeneration.toString.limitElements`：限制陣列/集合/對應中要列出的項目數，如果為 0 則列出所有項目。預設為 `0`。
* `java.selectionRange.enabled`：啟用/停用 Java 的智慧選取支援。停用此選項不會影響 VS Code 內建的基於單詞和括號的智慧選取。
* `java.showBuildStatusOnStart.enabled`：啟動時自動顯示建置狀態，預設為 `notification`。
  - `notification`：透過進度通知顯示建置狀態。
  - `terminal`：透過終端機顯示建置狀態。
  - `off`：不顯示任何建置狀態。
  > 為了向後相容，此設定也接受布林值，其中 `true` 與 `notification` 意義相同，`false` 與 `off` 意義相同。
* `java.project.outputPath`：儲存編譯輸出之工作區的相對路徑。`僅`在 `WORKSPACE` 範圍內有效。此設定 `不會` 影響 Maven或 Gradle 專案。
* `java.project.referencedLibraries`：設定 glob 模式，用於參考 Java 專案的本機程式庫。
* `java.completion.maxResults`：補完結果的最大數量（不包括程式碼片段）。`0`（預設值）表示停用限制，將傳回所有結果。如果遇到效能問題，請考慮設定一個合理的限制。
* `java.configuration.runtimes`：將 Java 執行環境對應到本機 JDK。
* `java.server.launchMode`：
  - `Standard`：提供完整功能，如智慧感知、重構、建置、Maven/Gradle 支援等。
  - `LightWeight`：以較低的啟動成本啟動語法伺服器。僅提供語法功能，如大綱、導覽、javadoc、語法錯誤。輕量模式不會載入第三方擴充套件，如 java 測試執行器、java 偵錯器等。
  - `Hybrid`：提供完整功能並具有更好的回應性。它會啟動一個標準語言伺服器和一個輔助的語法伺服器。語法伺服器提供語法功能，直到標準伺服器準備就緒。標準伺服器完全準備就緒後，語法伺服器將自動關閉。

預設啟動模式為 `Hybrid`。舊版模式為 `Standard`。
* `java.sources.organizeImports.starThreshold`：指定在使用星號匯入宣告前新增的匯入數量，預設為 99。
* `java.sources.organizeImports.staticStarThreshold`：指定在使用星號匯入宣告前新增的靜態匯入數量，預設為 99。
* `java.import.gradle.wrapper.checksums`：定義允許/不允許的 Gradle 包裝器 SHA-256 校驗和。
* `java.project.importOnFirstTimeStartup`：指定首次在混合模式下開啟資料夾時，是否匯入 Java 專案。支援的值為 `disabled`（永不匯入）、`interactive`（詢問是否匯入）、`automatic`（總是匯入）。預設為 `automatic`。
* `java.project.importHint`：當啟動時跳過 Java 專案匯入時，啟用/停用伺服器模式切換資訊。預設為 `true`。
* `java.import.gradle.java.home`：指定用於執行 Gradle 常駐程式的 JVM 位置。
* `java.project.resourceFilters`：從 Java 語言伺服器的重新整理中排除檔案和資料夾，這可以提高整體效能。例如，["node_modules","\.git"] 將排除所有名為 'node_modules' 或 '.git' 的檔案和資料夾。模式表示式必須與 `java.util.regex.Pattern` 相容。預設為 ["node_modules","\.git"]。
* `java.templates.fileHeader`：為新 Java 檔案指定檔案標頭註解。支援使用字串陣列設定多行註解，並使用 ${variable} 參考[預定義變數](https://github.com/redhat-developer/vscode-java/wiki/Predefined-Variables-for-Java-Template-Snippets)。
* `java.templates.typeComment`：為新 Java 類型指定類型註解。支援使用字串陣列設定多行註解，並使用 ${variable} 參考[預定義變數](https://github.com/redhat-developer/vscode-java/wiki/Predefined-Variables-for-Java-Template-Snippets)。
* `java.references.includeAccessors`：在尋找參考時包含 getter、setter 和 builder/constructor。預設為 true。
* `java.configuration.maven.globalSettings`：Maven 的 global settings.xml 路徑。
* `java.configuration.maven.lifecycleMappings`：Maven 的 lifecycle mappings xml 路徑。
* `java.eclipse.downloadSources`：為 Eclipse 專案啟用/停用下載 Maven 原始碼成品。
* `java.references.includeDecompiledSources`：在尋找參考時包含反編譯的原始碼。預設為 true。
* `java.project.sourcePaths`：儲存原始碼檔案之工作區的相對路徑。`僅`在 `WORKSPACE` 範圍內有效。此設定 `不會` 影響 Maven 或 Gradle 專案。
* `java.typeHierarchy.lazyLoad`：啟用/停用類型階層中的內容延遲載入。延遲載入可以節省大量載入時間，但每個類型都必須手動展開以載入其內容。
* `java.codeGeneration.insertionLocation`：指定由原始碼操作產生的程式碼的插入位置。預設為 `afterCursor`。
  - `afterCursor`：在游標所在的成員之後插入產生的程式碼。
  - `beforeCursor`：在游標所在的成員之前插入產生的程式碼。
  - `lastMember`：將產生的程式碼作為目標類型的最後一個成員插入。
* `java.codeGeneration.addFinalForNewDeclaration`：是否為建立新宣告的程式碼操作產生 'final' 修飾符。預設為 `none`。
  - `none`：不產生 final 修飾符
  - `fields`：僅為新欄位宣告產生 'final' 修飾符
  - `variables`：僅為新變數宣告產生 'final' 修飾符
  - `all`：為所有新宣告產生 'final' 修飾符
* `java.settings.url`：指定工作區 Java 設定的 url 或檔案路徑。請參閱 [設定全域偏好設定](https://github.com/redhat-developer/vscode-java/wiki/Settings-Global-Preferences)
* `java.symbols.includeSourceMethodDeclarations`：在符號搜尋中包含原始碼檔案的方法宣告。預設為 `false`。
* `java.quickfix.showAt`：在問題或行層級顯示快速修復。
* `java.configuration.workspaceCacheLimit`：保留未使用的作區快取資料的天數（如果啟用）。超過此限制，快取的作區資料可能會被移除。
* `java.import.generatesMetadataFilesAtProjectRoot`：指定是否在專案根目錄產生專案中繼資料檔案（.project、.classpath、.factorypath、.settings/）。預設為 `false`。
* `java.inlayHints.parameterNames.enabled`：啟用/停用參數名稱的內嵌提示。支援的值為：`none`（停用參數名稱提示）、`literals`（僅對字面參數啟用參數名稱提示）和 `all`（對字面和非字面參數啟用參數名稱提示）。預設為 `literals`。
* `java.inlayHints.parameterTypes.enabled`：啟用/停用（lambda）參數類型的內嵌提示。預設為 `false`。
* `java.compile.nullAnalysis.nonnull`：指定用於空值分析的 Nonnull 註釋類型。如果指定了多個註釋，則如果專案相依性中存在，將首先使用最頂層的註釋。如果 `java.compile.nullAnalysis.mode` 設定為 `disabled`，此設定將被忽略。
* `java.compile.nullAnalysis.nullable`：指定用於空值分析的 Nullable 註釋類型。如果指定了多個註釋，則如果專案相依性中存在，將首先使用最頂層的註釋。如果 `java.compile.nullAnalysis.mode` 設定為 `disabled`，此設定將被忽略。
* `java.compile.nullAnalysis.nonnullbydefault`：指定用於空值分析的 NonNullByDefault 註釋類型。如果指定了多個註釋，則如果專案相依性中存在，將首先使用最頂層的註釋。如果 `java.compile.nullAnalysis.mode` 設定為 `disabled`，此設定將被忽略。
* `java.import.maven.offline.enabled`：啟用/停用 Maven 離線模式。預設為 `false`。
* `java.edit.validateAllOpenBuffersOnChanges`：指定在編輯 Java 檔案時是否重新檢查所有開啟的 Java 檔案以獲取診斷資訊。預設為 `false`。
* `java.editor.reloadChangedSources`：指定當其來源 jar 檔案變更時是否重新載入開啟類別檔案的原始碼。預設為 `ask`。
  - `ask`：詢問是否重新載入開啟類別檔案的原始碼
  - `auto`：自動重新載入開啟類別檔案的原始碼
  - `manual`：手動重新載入開啟類別檔案的原始碼
* `java.edit.smartSemicolonDetection.enabled`：定義 `智慧分號` 偵測。預設為 `false`。
* `java.configuration.detectJdksAtStart`：啟動時自動偵測本機上安裝的 JDK。如果您在 `java.configuration.runtimes` 中指定了相同的 JDK 版本，擴充套件將優先使用該版本。預設為 `true`。
* `java.completion.collapseCompletionItems`：啟用/停用補完項目中重載方法的摺疊。會覆寫 `java.completion.guessMethodArguments`。預設為 `false`。
* `java.diagnostic.filter`：指定一個檔案模式列表，符合的文件將不回報其診斷資訊（例如 `\*\Foo.java`）。
* `java.search.scope`：指定用於搜尋操作的範圍，例如
  - 尋找參考
  - 呼叫階層
  - 工作區符號
* `java.jdt.ls.javac.enabled`：[實驗性] 指定是否在語言伺服器中啟用基於 Javac 的編譯。需要使用 Java 24 執行此擴充套件。預設為 `off`。
* `java.completion.engine`：[實驗性] 選擇程式碼補完引擎。預設為 `ecj`。
* `java.references.includeDeclarations`：在尋找參考時包含宣告。預設為 `true`。
* `java.jdt.ls.appcds.enabled`：[實驗性] 啟用 Java AppCDS（應用程式類別資料共享）以改善擴充套件啟動。當設定為 `auto` 時，AppCDS 將在 Visual Studio Code - Insiders 和預發行版本中啟用。

1.50.0 新功能
* `java.hover.javadoc.enabled`：啟用/停用懸停時顯示 Javadoc。預設為 `true`。

語意高亮
===============
[語意高亮](https://github.com/redhat-developer/vscode-java/wiki/Semantic-Highlighting) 修正了預設 Java Textmate 文法中的許多語法高亮問題。但是，您可能會遇到一些小問題，特別是當它啟動時會有延遲，因為它需要由 Java 語言伺服器在開啟新檔案或輸入時計算。可以使用 `editor.semanticHighlighting.enabled` 設定為所有語言停用，或使用[特定語言的編輯器設定](https://code.visualstudio.com/docs/getstarted/settings#_languagespecific-editor-settings)僅為 Java 停用。

疑難排解
===============
1. 檢查右下角語言工具的狀態（下圖中標有 A 的位置）。
它應該像下圖一樣顯示就緒（豎起大拇指）。您可以點擊狀態並開啟語言工具日誌以獲取有關失敗的更多資訊。

![ status indicator ](https://raw.githubusercontent.com/redhat-developer/vscode-java/main/images/statusMarker.png)

2. 閱讀[疑難排解指南](https://github.com/redhat-developer/vscode-java/wiki/Troubleshooting)以收集有關您可能遇到的問題的資訊。

3. 向[專案](https://github.com/redhat-developer/vscode-java/issues)回報您遇到的任何問題。

貢獻
===============
這是一個對任何人開放的開源專案。非常歡迎貢獻！

有關入門資訊，請參閱 [CONTRIBUTING 說明](CONTRIBUTING.md)。

可以從 http://download.jboss.org/jbosstools/jdt.ls/staging/](http://download.jboss.org/jbosstools/jdt.ls/staging/?C=M;O=D) 安裝持續整合建置。下載最新的 `java-<version>.vsix` 檔案，並按照[此處](https://code.visualstudio.com/docs/editor/extension-gallery#_install-from-a-vsix)的說明進行安裝。
穩定版本存檔在 http://download.jboss.org/jbosstools/static/jdt.ls/stable/。

此外，您可以按照[此處](https://github.com/redhat-developer/vscode-java/wiki/Contribute-a-Java-Extension)的說明貢獻您自己的 VS Code 擴充套件以增強現有功能。

回饋
===============
* 有問題嗎？在 [GitHub Discussions](https://github.com/redhat-developer/vscode-java/discussions) 開始討論，
* 在 [GitHub Issues](https://github.com/redhat-developer/vscode-java/issues) 提交錯誤，
* 在 [Gitter](https://gitter.im/redhat-developer/vscode-java) 上與我們聊天，
* [發推文給我們](https://twitter.com/VSCodeJava/) 以提供其他回饋。

授權
===============
EPL 2.0，詳情請參閱 [LICENSE](LICENSE)。
