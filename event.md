# Event

#API

和Event相关的API巨多

```javascript
.bind() //不建议使用 和.on类似
.blur() //绑定或触发失去焦点
.change() //
.click()
.contextmenu()
.dbclick()
.delegate()
.die()
.error()
event.currentTarget
event.data
event.delegateTarget
event.isDefaultPrevented()
event.isImmediatePropagationStopped()
event.isPropagationStopped()
event.metaKey
event.namespace
event.pageX
event.pageY
event.preventDefault()
event.relatedTarget
event.result
event.stopImmediatePropagation()
event.stopPropagation()
event.target
event.timeStamp
event.type
event.which
.focus()
.focusin()
.focusout()
.hover()
jQuery.proxy()
.keydown()
.keypress()
.keyup()
.mousedown()
.mouseenter()
.mouseleave()
.mousemove()
.mouseout()
.mouseover()
.mouseup()
.off()
.on()
.one()
.ready()
.resize()
.scroll()
.select()
.submit()
.toggle()
.trigger()
.triggerHandler()
.unbind()
.undelegate()

```

# 结构

```javascript
function on ( elem, types, selector, data, fn, one){}

jQuery.event = {
    global: {},
    //绑定一个或多个类型的事件监听函数
    add: function( elem, types, handler, data, selector ) {},
    //移除一个或多个类型的事件监听函数
    remove: function (elem, types, handler, selector, mappedTypes){},
    //分法事件,执行事件监听函数
    dispatch: function ( nativeEvent) {},
    //
    handlers: function( event, handles) {},
    //添加事件对象的公共属性
    addProp: function( name, hook){},
    //把原生的事件对象封装成jQuery对象,并修正不兼容属性
    fix: function( originalEvent ){},
    //事件修正对象集
    special: {
        load: {},
        focus: {
            tirgger: function(){},
            delegateType: "focusin"
        },//
        blur: {
            tirgger: function(){},
            delegateType: "focusout"
        },
        click: {
            trigger: function(){},
            _default: function ( event ){}
        },
        beforeunload: {
            postDispatch: function( event ){}
        }
    }
}

//移除监听函数
jQuery.removeEvent = function( elem, type, handle ) {}

//事件对象
jQuery.Event = function( src, props ) {}

//原型对象
jQuery.Event.prototype = {
	constructor: jQuery.Event,
	isDefaultPrevented: returnFalse,
	isPropagationStopped: returnFalse,
	isImmediatePropagationStopped: returnFalse,
	isSimulated: false,
	preventDefault: function() {},
	stopPropagation: function() {},
	stopImmediatePropagation: function() {}
}

// Includes all common event props including KeyEvent and MouseEvent specific props
jQuery.each( {
	altKey: true,
	bubbles: true,
	cancelable: true,
	changedTouches: true,
	ctrlKey: true,
	detail: true,
	eventPhase: true,
	metaKey: true,
	pageX: true,
	pageY: true,
	shiftKey: true,
	view: true,
	"char": true,
	charCode: true,
	key: true,
	keyCode: true,
	button: true,
	buttons: true,
	clientX: true,
	clientY: true,
	offsetX: true,
	offsetY: true,
	pointerId: true,
	pointerType: true,
	screenX: true,
	screenY: true,
	targetTouches: true,
	toElement: true,
	touches: true,

	which: function( event ) {
	    ...
	    return event.which;
	}
}, jQuery.event.addProp );

jQuery.each( {
	mouseenter: "mouseover",
	mouseleave: "mouseout",
	pointerenter: "pointerover",
	pointerleave: "pointerout"
}, function( orig, fix ) {
	jQuery.event.special[ orig ] = {
		delegateType: fix,
		bindType: fix,

		handle: function( event ) {}
	};
} );

jQuery.fn.extend( {

	on: function( types, selector, data, fn ) {
		return on( this, types, selector, data, fn );
	},
	one: function( types, selector, data, fn ) {
		return on( this, types, selector, data, fn, 1 );
	},
	off: function( types, selector, fn ) {}
	}
} );
```