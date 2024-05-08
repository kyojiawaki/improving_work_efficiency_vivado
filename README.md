# vivadoの作業効率化

# rpt2sp: rptファイルからスプレッドシートへの変換スクリプト

rpt2spは、Google Apps Scriptを使用してrptファイルからデータを抽出し、Googleスプレッドシートに書き込むためのスクリプトです。

## 使用法

1. このスクリプトをGoogle Apps Scriptとして作成します。
2. Google Apps Scriptエディタでスクリプトをペーストします。
3. スクリプト内の`rpt2spConstants`オブジェクトを適宜編集し、シート名、フォルダ名、ファイル名などを設定します。
4. スクリプトを実行します。

## rpt2spConstantsオブジェクト

```javascript
const rpt2spConstants = {
  sheetName: 'txt2sp',
  folderName: 'rpt2sp',
  fileNames: {
    utilization: 'DPU_utilization_placed.rpt',
    power: 'DPU_power_routed.rpt',
    timing: 'DPU_timing_summary_routed.rpt'
  },
  extStrings: {
    utilization: {
      LUT: /\|   LUT as Logic          \|(.*?)\|/,
      LUTRAM: /\|   LUT as Memory         \|(.*?)\|/,
      FF: /\|   Register as Flip Flop \|(.*?)\|/,
      DSP: /\| DSPs      \|(.*?)\|/
    },
    power: {
      Dynamic: /\|\s*Dynamic \(W\)\s*\|\s*([\d.]+)\s*\|/,
      Static: /\|\s*Device Static \(W\)\s*\|\s*([\d.]+)\s*\|/
    },
    timing: {
      WNS: /Setup :\s.*  Failing Endpoints,  Worst Slack\s+(.*?)\s*,/,
      WHS: /Hold  :\s.*  Failing Endpoints,  Worst Slack\s+(.*?)\s*,/,
      WPWS: /PW    :\s.*  Failing Endpoints,  Worst Slack\s+(.*?)\s*,/
    }
  },
  columns: [
    'TimeStamp',
    'LUT',
    'LUTRAM',
    'FF',
    'DSP',
    'Dynamic',
    'Static',
    'WNS',
    'WHS',
    'WPWS'
  ]
};
