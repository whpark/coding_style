# C# Naming Convention

## 1. 타입


| 종류 | 접두어 | 예 |
|---|---|---|
| class (일반·static) | `x` | `xProject`, `xRecipe`, `xBellDetector`, `xCsvMeasurementStore` |
| record class | `rx` | `rxBellShape`, `rxSignalFilterDefinition`, `rxChrMeasurementBatch` |
| record struct | `rs` | `rsEncoderScanGeometry`, `rsChrSampleLayout` |
| struct | `s` | `sPoint3D`, `sRect2D`, `sRadian`, `sColorRGBA` |
| interface, abstract | `I` | `ICommandServer`, `IRecipeEditor` |
| enum | `e` + `UPPER_SNAKE_CASE` | `eSIGNAL_FILTER_TYPE`, `eCHR_DEVICE_STATE` |
| generic type parameter | `T` | `WriteJson<T>` |
| Form | `Form`으로 시작 | `FormRecipe`, `FormMeasurement` |
| WPF Window | `xWnd` | `xWndMain`, `xWndPaste` |
| UserControl | `Ctrl`로 시작 | `CtrlPlotPanel`, `CtrlSpectrum`, `CtrlCrossSection` |

접두어를 뺀 나머지는 PascalCase.

**예외** — `MainForm`, `MainWnd` (historical reason)

## 2. 멤버

| 대상 | 규칙 | 예 |
|---|---|---|
| 가변 필드 (접근성 무관) | `m_` + camelCase, hungarian (아래 참조) | `m_bBusy`, `m_recipeCurrent`, `m_bUpdate` |
| struct 의 필드 | `m_` 없이 camelCase | `x`, `y`, `pt0`, `width` |
| `const` | `UPPER_SNAKE_CASE` | `MAX_LOG_ENTRIES`, `DEFAULT_EXTENSION` |
| 속성 / 메서드 / 이벤트 | PascalCase | `CurrentRecipe`, `AppendLog` |
| 지역변수 / 파라미터 | camelCase | `recipe`, `countsPerMillimeter` |

## 3. enum 타입 변수

**타입이 enum이면 이름을 `e`로 시작한다.** 필드·속성·파라미터·지역변수·패턴변수 모두 해당.

```csharp
public eCHR_CONNECTION_MODE eConnectionMode { get; set; }   // 속성
private eCHR_DEVICE_STATE m_eState;                          // 필드는 m_ 와 함께
void OnStateChanged(eCHR_DEVICE_STATE eState) { ... }        // 파라미터
var eState = xProject.ChrDevice.eState;                      // 지역변수
if (x is eCHR_SPECTRUM_TYPE eType) { ... }                   // 패턴변수
```

## 4. Hungarian 타입 약어

| 타입 | 약어 | 예 |
|---|---|---|
| `bool` | `b` | `m_bUpdate` |
| index(int,long,int64...) | `i` | `m_iTest`, 예외: (int index;) |
| 갯수(int,long,int64...) | `n` | `m_nItem` |
| `string` | `str` | `m_strRecipeFolder` |
| `StringBuilder` | `sb` | `m_sbSQL` |
| `double` | `d` | `m_dCountsPerMillimeter` |
| enum | `e` | `m_eState` |
| struct/class/interface/record 등 | 타입이름약어 | `m_recipeCurrent` |

historical reason 으로 사용하고 있는 약간의 예외는 그대로 사용.


## 5. UI control

`.Designer.cs`에 선언하고 `ui_` + 종류 약어를 붙인다.

```
ui_spin  NumericUpDown      ui_cmb   ComboBox        ui_txt   TextBox
ui_btn   Button             ui_lbl   Label           ui_chk   CheckBox
ui_radio RadioButton        ui_grp   GroupBox        ui_pnl   Panel/TableLayout/FlowLayout
ui_tab   TabControl         ui_page  TabPage         ui_lst   ListView/ListBox
ui_dgv   DataGridView       ui_timer Timer
```
