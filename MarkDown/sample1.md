20250530

#### tail sample:
解釋 tail -f $QTCPSERVICE_DIR/logs/$LAST_LOG_FILE | grep -a -E "B\ parameter\ parse\ failed|\ recv\ timeout|CloseConnection\ sid|OnDisconnected| TcpSession\ disconnected|RemoveConnection\ sid|Total\ connection\ count|OnRecv|\ -\ sessionId|/commannd|dRC|dEC"

trace3.sh:
#!/bin/bash
QTCPSERVICE_DIR=/home/quandic/Projects/QTCPService
LAST_LOG_FILE=$(ls -l $QTCPSERVICE_DIR/logs | tail -1 | awk '{print $9}')
echo "The last log file is $LAST_LOG_FILE"
tail -f $QTCPSERVICE_DIR/logs/$LAST_LOG_FILE | grep -a -E "B\ parameter\ parse\ failed|\ recv\ timeout|CloseConnection\ sid|OnDisconnected| TcpSession\ disconnected|RemoveConnection\ sid|Total\ connection\ count|OnRecv|\ -\ sessionId|/commannd|dRC|dEC"


$ ./trace3.sh
The last log file is 20250521_145152.log
2025-05-29 11:31:14.1596| [ReaderOperator] sid: 95 +OnRecv: (132) $0001400000011234560118012828b10019786630020887631021437631600047730021037731021507831019377930020877931008537930600028030E090h000
2025-05-29 11:31:24.1053| [ReaderOperator] sid: 95 +OnRecv: (132) $0001400000011234560113012839b10019786530020887531019167530021437631021037731020877831021507931019377930600027930600047930E090h000
2025-05-29 11:31:34.1509| [ReaderOperator] sid: 95 +OnRecv: (132) $0001400000011234560108012849b10019786830008537230021437431019167530600027630600047630600067730600017730600007730020877731E090h000
2025-05-29 11:31:46.1805| [ReaderOperator] sid: 95 +OnRecv: (132) $0001400000011234560108012901b10019786530021297631021237631021317631600047630008537730019167730020887831600017930020877931E090h000
2025-05-29 11:31:57.1733| [ReaderOperator] sid: 95 +OnRecv: (132) $0001400000011234560119012912b10019786130019166630600067130600017230020877431021377531020887531600047630600027630600007730E090h000
2025-05-29 11:32:07.1236| [ReaderOperator] sid: 95 +OnRecv: (132) $0001400000011234560113012922b10019786030019167030008537330020887431021437531600047630600017730021507731600067830021037831E090h000
2025-05-29 11:32:18.1692| [ReaderOperator] sid: 95 +OnRecv: (132) $0001400000011234560110012933b10019786230019167130021037431021437531020877631600067630020887631600047630600017730019377730E090h000


解釋 tail -f $QTCPSERVICE_DIR/logs/$LAST_LOG_FILE | grep -a -E "B\ parameter\ parse\ failed|\ recv\ timeout|CloseConnection\ sid|OnDisconnected| TcpSession\ disconnected|RemoveConnection\ sid|Total\ connection\ count|OnRecv|\ -\ sessionId|/commannd|dRC|dEC"
這條指令的作用是**即時監控某個日誌檔案的內容，並過濾出特定關鍵字或錯誤訊息**。我們來逐步拆解這條指令的意思：

```bash
tail -f $QTCPSERVICE_DIR/logs/$LAST_LOG_FILE | grep -a -E "B\ parameter\ parse\ failed|\ recv\ timeout|CloseConnection\ sid|OnDisconnected| TcpSession\ disconnected|RemoveConnection\ sid|Total\ connection\ count|OnRecv|\ -\ sessionId|/commannd|dRC|dEC"
```

### 1. `tail -f $QTCPSERVICE_DIR/logs/$LAST_LOG_FILE`
- `tail -f`：持續監控檔案的新增內容（即「追蹤」模式），常用於觀察日誌檔。
- `$QTCPSERVICE_DIR/logs/$LAST_LOG_FILE`：這是日誌檔案的完整路徑，由環境變數組成。假設：
  - `$QTCPSERVICE_DIR` 是服務的根目錄
  - `$LAST_LOG_FILE` 是最新的日誌檔名

### 2. `| grep -a -E "..."`：
- `|`：管道符號，將 `tail -f` 的輸出傳給 `grep`。
- `grep`：用來搜尋符合條件的文字。
- `-a`：將檔案視為文字檔（即使是二進位檔也會當作文字處理）。
- `-E`：使用「擴展正則表達式」（Extended Regular Expressions），允許使用 `|` 來表示「或」的邏輯。

### 3. `"..."`：正則表達式，用來匹配以下關鍵字或訊息：
這些訊息通常與 TCP 連線、封包處理、錯誤或斷線有關：

- `B parameter parse failed`：參數解析失敗
- `recv timeout`：接收逾時
- `CloseConnection sid`：關閉連線（指定 session ID）
- `OnDisconnected`：斷線事件
- `TcpSession disconnected`：TCP 會話中斷
- `RemoveConnection sid`：移除連線（指定 session ID）
- `Total connection count`：總連線數
- `OnRecv`：接收到資料
- `- sessionId`：包含 sessionId 的訊息
- `/commannd`：可能是 `/command` 的拼寫錯誤？
- `dRC`、`dEC`：可能是某些自訂協議的縮寫（例如 decode/receive code）

---

指令的用途是**即時監控 TCP 服務的日誌檔案，並過濾出與連線、封包、錯誤處理等相關的訊息**，方便開發者或運維人員快速定位問題。

