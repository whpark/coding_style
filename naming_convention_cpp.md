# cpp Naming Convention

## 1. 타입


| 종류 | naming | ex |
|---|---|---|
| class | prefix `x` | `xProject`, `xWndMain`, `xAppNabi` |
| struct | prefix  `s` | `sPoint3D`, `sRect2D`, `sDegree`, `sColorRGBA` |
| interface class (pure virtual) | prefix `I` | | `ICommandServer`, `IRecipeEditor` |
| class/struct typename alias | postfix `_t` | using point_t = sPoint3D; |
| template class | `T` | template < typename tValue, size_t DIMENSION > TPoint { ... }; |
| enum | e`UPPER_SNAKE_CASE` | `eDEVICE_TYPE`, `eCOLOR_INDEX` |

| UI Class | naming | --- |
|---|---|---|
| Window | prefix `xWnd` | `xWndMain`, `xWndPaste` |
| User Control (Window 내부에 들어가는 Control) | prefix `xCtrl` | `xCtrlPlotPanel`, `xCtrlSpectrum`, `xCtrlCrossSection` |
| Dialog (modal / modeless) | prefix `xDlg` | `xDlgInformation` ... |

접두어를 뺀 나머지는 PascalCase.

## 2. 멤버

| 대상 | 규칙 | 예 |
|---|---|---|
| member variable | `m_` + camelCase, hungarian (아래 참조) | `m_bBusy`, `m_recipeCurrent`, `m_bUpdate` |
| struct 의 필드 | `m_` 없이 camelCase | `x`, `y`, `pt0`, `width` |
| `const` | `UPPER_SNAKE_CASE` | `MAX_LOG_ENTRIES`, `DEFAULT_EXTENSION` |
| 메서드 / 이벤트 | PascalCase | `CurrentRecipe`, `AppendLog` |
| 지역변수 / 파라미터 | camelCase | `recipe`, `countsPerMillimeter` |

## 3. enum 타입 변수

**타입이 enum이면 이름을 `e`로 시작한다.** 필드·속성·파라미터·지역변수·패턴변수 모두 해당.

```cpp
eCHR_CONNECTION_MODE eConnectionMode{};
eCHR_DEVICE_STATE m_eState;                          // 필드는 m_ 와 함께
void OnStateChanged(eCHR_DEVICE_STATE eState) { ... }        // 파라미터
auto eState = m_project.m_chrDevice.eState;                  // 지역변수
```

## 4. Hungarian 타입 약어

| 타입 | 약어 | 예 |
|---|---|---|
| `bool` | `b` | `m_bUpdate` |
| index(int,long,int64...) | `i` | `m_iTest`, 예외: (int index;) |
| 갯수(int,long,int64...) | `n` | `m_nItem` |
| `u8string` | `u8` | `m_u8strRecipeFolder` |
| `wstring` | `wstr` | `m_wstrRecipeFolder` |
| `string` | `str` | `m_strRecipeFolder` |
| `double` | `d` | `m_dCountsPerMillimeter` |
| enum | `e` | `m_eState` |
| std::mutex | `mtx` | |
| std::thread | `thread` | |
| struct/class/interface/record 등 | 타입이름약어 | `m_recipeCurrent` |
| 스레드 작업 함수 | PascalCase로 작업 역할 표현 | `ImageLoader`, `ImageDecoder`, `ZipExtractor`, `ChapterFinder`, `ZipFiles` |

historical reason 으로 사용하고 있는 약간의 예외는 그대로 사용.


## 5. UI control

`.ui`에서 지정하는 `objectName`은 **종류 약어 + 용도(PascalCase)**로 작성한다. `m_` 접두어는 사용하지 않는다.

예: `btnExecuteCommand`, `chkAutoStart`, `cmbHistory`.

기존 컨트롤 이름과 약어는 유지하며, 새 컨트롤은 아래 목록을 따른다.

### 5.1. Qt 위젯

| Qt 클래스 | 약어 | 이름 예시 |
|---|---|---|
| `QWidget` | `ctrl` | `ctrlPreview` |
| `QMainWindow` | `wnd` | `wndMain` |
| `QDialog` | `dlg` | `dlgSettings` |
| `QFrame` | `ctrl` | `ctrlPreview` |
| `QPushButton`, `QToolButton` | `btn` | `btnRefresh` |
| `QRadioButton` | `rbtn` | `rbtnHorizontal` |
| `QCheckBox` | `chk` | `chkAutoScroll` |
| `QDialogButtonBox` | `btnbox` | `btnboxSettings` |
| `QCommandLinkButton` | `lnk` | `lnkOpenFolder` |
| `QLabel` | `lbl` | `lblStatus` |
| `QLineEdit` | `txt` | `txtFolderPath` |
| `QTextEdit` | `txt` | `txtDescription` |
| `QPlainTextEdit` | `txt` | `txtLog` |
| `QTextBrowser` | `browser` | `browserHelp` |
| `QComboBox`, `QFontComboBox` | `cmb` | `cmbHistory`, `cmbFont` |
| `QSpinBox`, `QDoubleSpinBox` | `spin` | `spinPageCount`, `spinZoom` |
| `QDateEdit` | `date` | `dateStart` |
| `QTimeEdit` | `time` | `timeStart` |
| `QDateTimeEdit` | `dt` | `dtScheduled` |
| `QCalendarWidget` | `cal` | `calBookmark` |
| `QSlider` | `slider` | `sliderZoom` |
| `QDial` | `dial` | `dialRotation` |
| `QScrollBar` | `sb` | `sbPage` |
| `QProgressBar` | `progress` | `progressLoading` |
| `QLCDNumber` | `lcd` | `lcdPageCount` |
| `QListView`, `QListWidget` | `lst` | `lstChapters` |
| `QTreeView`, `QTreeWidget` | `tree` | `treeFolders` |
| `QTableView`, `QTableWidget` | `tbl` | `tblBookmarks` |
| `QColumnView` | `colview` | `colviewFolders` |
| `QGraphicsView` | `view` | `viewImages` |
| `QOpenGLWidget` | `gl` | `glCanvas` |
| `QGroupBox` | `grp` | `grpViewOptions` |
| `QTabWidget`, `QTabBar` | `tab` | `tabViewer`, `tabNavigation` |
| `QStackedWidget` | `stack` | `stackBrowser` |
| `QScrollArea` | `area` | `areaImages` |
| `QSplitter` | `split` | `splitPreview` |
| `QToolBox` | `toolbox` | `toolboxOptions` |
| `QDockWidget` | `dock` | `dockFolders` |
| `QMdiArea` | `mdi` | `mdiViewers` |
| `QMdiSubWindow` | `wnd` | `wndViewer` |
| `QMenuBar` | `menubar` | `menubarMain` |
| `QMenu` | `menu` | `menuFile` |
| `QToolBar` | `toolbar` | `toolbarViewer` |
| `QStatusBar` | `statusbar` | `statusbarMain` |
| `QWebEngineView` (Qt WebEngine) | `web` | `webBrowser` |

### 5.2. 액션 및 그룹

| Qt 클래스 | 약어 | 이름 예시 |
|---|---|---|
| `QAction` | `action` | `actionOpen` |
| `QButtonGroup` | `btngrp` | `btngrpViewType` |

### 5.3. 레이아웃 및 간격

| Qt 클래스 | 약어 | 이름 예시 |
|---|---|---|
| `QVBoxLayout` | `vbox` | `vboxMain` |
| `QHBoxLayout` | `hbox` | `hboxNavigation` |
| `QGridLayout` | `grid` | `gridOptions` |
| `QFormLayout` | `form` | `formSettings` |
| `QStackedLayout` | `stklayout` | `stklayoutPages` |
| `QSpacerItem` | `spacer` | `spacerBottom` |

## 7. Qt 콜백 및 시그널 (BiscuitView 사용 예)

| 대상 | 규칙 | 예 |
|---|---|---|
| Qt 가상 함수 override | Qt 원래 함수 이름 유지 | `closeEvent`, `moveEvent`, `resizeEvent`, `keyPressEvent` |
| UI 이벤트 처리 메서드 | `On` + PascalCase, 기존 구분용 `_` 유지 | `OnBtnRefresh`, `OnTimer_UI`, `OnButtonClick_ChapterNext` |
| Qt 시그널 | `sig` + PascalCase | `sigFolderChanged` |
| 함수 객체 / 콜백 멤버 | `m_fn` + 동작, struct 내부는 `fn` + 동작 | `m_fnRefreshBookmark`, `fnOpenBrowser`, `fnJumpToComics` |

Qt override 이름과 기존 이벤트 처리 이름은 프레임워크 계약 및 historical 예외로 유지한다.
