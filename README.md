## 流程說明
👉 [點此查看互動式流程圖] https://cicicode.github.io/power-automate-portfolio/

## 附加至字串變數
'''
concat(
'<tr>',

'<td style="padding:6px 40px 6px 6px;">',
if(
    greaterOrEquals(indexOf(items('For_each')?['subject'],'流通在外'),0),
    substring(
        items('For_each')?['subject'],
        12,
        sub(indexOf(items('For_each')?['subject'],'流通在外'),12)
    ),
    '（無法解析單位）'
),
'</td>',

'<td style="padding:6px 40px 6px 6px;">',
formatDateTime(items('For_each')?['receivedDateTime'], 'yyyy/MM/dd'),
'</td>',

'<td style="padding:6px 40px 6px 6px;"></td>',

'<td style="padding:6px 40px 6px 6px;"></td>',

'<td style="padding:6px 6px 6px 6px;">',
items('For_each')?['subject'],
'</td>',
'<td style="padding:6px 6px 6px 6px;">',
trim(
    substring(
        items('For_each')?['body'],
        add(indexOf(items('For_each')?['body'],'20'),13),
        sub(
            indexOf(items('For_each')?['body'],'謝謝'),
            add(indexOf(items('For_each')?['body'],'20'),13)
        )
    )
),
'</td>',

'</tr>'
)

## 傳送至電子郵件(V2)
'''
concat(
'本月通知清單：<br><br>
<table style="border-collapse:collapse; font-family:Consolas, monospace; font-size:13px;">
<tr>
<th style="text-align:left; padding:6px 40px 6px 6px;">單位名稱</th>
<th style="text-align:left; padding:6px 40px 6px 6px;">通知日期</th>
<th style="text-align:left; padding:6px 40px 6px 6px;">是否回覆</th>
<th style="text-align:left; padding:6px 40px 6px 6px;">回覆時間</th>
<th style="text-align:left; padding:6px 6px 6px 6px;">主旨</th>
<th style="text-align:left; padding:6px 6px 6px 6px;">內容摘要</th>
</tr>',
variables('mailBody'),
'</table>'
)
