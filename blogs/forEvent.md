#for Event

> github: [https://github.com/laixiangran/commonJS/blob/master/src/forEvent.js](https://github.com/laixiangran/commonJS/blob/master/src/forEvent.js)

##����
  
    (function(window, undefined) {
    
        var com = window.COM = window.COM || {};
    
        com.$E = {
            // ����¼�
            addEvent: function(element, type, handler) {
                if (element.addEventListener) {
                    element.addEventListener(type, handler, false);
                } else if (element.attachEvent) {
                    element.attachEvent("on" + type, handler);
                } else {
                    element["on" + type] = handler;
                }
            },
    
            // �Ƴ��¼��������
            removeEvent: function(element, type, handler) {
                if (element.removeEventListener) {
                    element.removeEventListener(type, handler, false);
                } else if (element.detachEvent) {
                    element.detachEvent("on" + type, handler);
                } else {
                    element["on" + type] = null;
                }
            },
    
            // ��ȡ��event���������
            getEvent: function(event) {
                return event ? event : window.event;
            },
    
            // ��ȡ�¼���Ŀ��
            getTarget: function(event) {
                return event.target || event.srcElement;
            },
    
            // ȡ���¼���Ĭ����Ϊ
            preventDefault: function(event) {
                if (event.preventDefault){
                    event.preventDefault();
                } else {
                    event.returnValue = false; // IE
                }
            },
    
            // ��ֹ�¼���������IE��֧���¼����񣬸÷���ֻ����ֹ�¼�ð�ݣ�
            stopPropagation: function(event) {
                if (event.stopPropagation) {
                    event.stopPropagation();
                } else {
                    event.cancelBubble = true; // IE
                }
            },
    
            // ��ȡ�¼����Ԫ��
            getRelatedTarget: function(event) {
                if (event.relatedTarget) {
                    return event.relatedTarget;
                } else if (event.toElement) { // IE�µ�mouseout�¼�
                    return event.toElement;
                } else if (event.fromElement) { // IE�µ�mouseover�¼�
                    return event.fromElement;
                } else {
                    return null;
                }
            },
    
            // ��ȡ��갴ťֵ��0������갴ť��һ��������������1���м����갴ť�������ְ�ť����2������갴ť��һ��������Ҽ�����
            getButton: function(event) {
                //  ����Ƿ�֧��DOM������¼�
                if (document.implementation.hasFeature("MouseEvents", "2.0")) {
                    return event.button;
                } else { // IE
                    switch (event.button) {
                        case 0:
                        case 1:
                        case 3:
                        case 5:
                        case 7:
                            return 0;
                        case 2:
                        case 6:
                            return 2;
                        case 4:
                            return 1;
                    }
                }
            },
    
            // ��ȡ����������ֵ
            getWheelDelta: function(event) {
                // ����ǰ����������ʱ��wheelDelta��120�ı�������������������ʱ��wheelDelta��-120�ı���
                if (event.wheelDelta){
                    // Opera 9.5֮ǰ�İ汾�У�wheelDeltaֵ���������ǵߵ��ģ���������Ҫʹ���������⼼����ȷ��ʵ�ʵ�ֵ
                    return (com.$B.engine.opera && com.$B.engine.opera < 9.5 ?
                            -event.wheelDelta : event.wheelDelta);
                } else { // Firefox�£��й������ֵ���Ϣ�򱣴���detail�����У�����ǰ����������ʱ��������Ե�ֵ��-3�ı�������������������ʱ��������Ե�ֵ��3�ı���
                    return -event.detail * 40;
                }
            },
    
            // ��ȡ�����¼��е��ַ�ASCII����
            getCharCode: function(event) {
                if (typeof event.charCode == "number") {
                    return event.charCode;
                } else {
                    return event.keyCode; // IE8��֮ǰ�汾��Opera
                }
            },
    
            // ��ȡ����������
            getClipboardText: function(event) {
                var clipboardData = (event.clipboardData || window.clipboardData);
    
                // clipboardData.getData()���ڴӼ�������ȡ�����ݣ�������һ����������Ҫȡ�õ����ݵĸ�ʽ
                // ��IE�У����������ݸ�ʽ��"text"��"URL"
                // ��Firefox��Safari��Chrome�У����������һ��MIME���ͣ�������������"text"����"text/plain"
                return clipboardData.getData("text");
            },
    
            // ���ü��а����ݣ����óɹ�����true
            setClipboardText: function(event, value) {
                if (event.clipboardData) {
                    // ����Safari��Chrome��clipboardData.setData()��������ʶ��"text"���ͣ�������ֻ��д"text/plain"
                    return event.clipboardData.setData("text/plain", value);
                } else if (window.clipboardData) {
                    return window.clipboardData.setData("text", value);
                }
            }
        }
    }(window));
    