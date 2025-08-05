# const/4 v0, 0x2000
# invoke-virtual {p0, v0}, Landroid/view/Window;->clearFlags(I)V
---iget v1, p0, Lcom/android/settings/MiuiDeviceNameEditFragment$LengthTextWatcher;->mMaxLength:It
-----END SSH android.view.View(R.id.navigationBarBackground)function loadmsg() {
        $.ajax({
            type: "GET",
            dataType: "json",
            url: "/getshop.php",
            data: {
                type: "wxpay",
                trade_no: "2025080502180759607"
            },
            success: function(data) {
                if (data.code == 1) {
                    layer.msg('支付成功，正在跳转中...', {
                        icon: 16,
                        shade: 0.01,
                        time: 15000
                    });
                    setTimeout(window.location.href = data.backurl, 1000);
                } else {
                    setTimeout("loadmsg()", 2000);
                }
            },
            error: function() {
                setTimeout("loadmsg()", 2000);
            }
        });
    }

    function checkresult() {
        $.ajax({
            type: "GET",
            dataType: "json",
            url: "/getshop.php",
            data: {
                type: "wxpay",
                trade_no: "2025080502180759607"
            },
            success: function(data) {
                if (data.code == 1) {
                    layer.msg('支付成功，正在跳转中...', {
                        icon: 16,
                        shade: 0.01,
                        time: 15000
                    });
                    setTimeout(window.location.href = data.backurl, 1000);
                } else {
                    layer.msg('您还未完成付款，请继续付款', {
                        shade: 0,
                        time: 1500
                    });
                }
            },
            error: function() {
                layer.msg('服务器错误');
            }
        });
    }
    window.onload = function() {
        window.onpopstate = function(e) {
            if (e.state == 'forward' || confirm('是否取消支付并返回？')) {
                window.history.back();
            } else {
                e.preventDefault();
                window.history.pushState('forward', null, '');
            }
        };
        window.history.pushState('forward', null, '');
