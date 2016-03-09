##��ͷ������

������C#����Java����϶�֪��lambda���ʽ��ES6�������ļ�ͷ������=>��������ͬ��֮������˺�������д�����������Ϊ����Ĳ��������ұ����ǽ��еĲ����Լ����ص�ֵInputs=>outputs��
����֪����JS�лص��Ǿ������£���һ��ص�����������������ʽ���֣�ÿ�ζ���Ҫдһ��function�����Ƿ������������ͷ����������Է����д�ص��ˡ��뿴��������ӣ�

    var array = [1,2,3];
    
    // ��ͳд��д��
    array.forEach(function(v) {
        console.log(v);
    });
    
    // ES6д��
    array.forEach(v => console.log(v));

##���֧��

ES6������˶����֧�֣�������class�� ���֣���ʵclass��JavaScript��һֱ�Ǳ����֣�Ŀ�ľ��ǿ��ǵ��������Ժ���°汾�л��õ����������������ó��ˣ���JS�������������� �ģ�ES6���ṩ����ʵ����ֻ��JSԭ��ģʽ�İ�װ�������ṩԭ����class֧�ֺ󣬶���Ĵ������̳и���ֱ���ˣ����Ҹ��෽���ĵ��ã�ʵ��������̬�� ���͹��캯���ȸ���������󻯡�

�������չʾ������ES6�е�ʹ�ã�

    // ��Ķ���
    class Animal {
        // ES6�����͹�����
        constructor(name) {
            this.name = name;
        }
    
        // ʵ������
        sayName() {
            console.log('My name is ' + this.name);
        }
    }
    
    // ��ļ̳�
    class Programmer extends Animal {
        constructor(name) {
            // ֱ�ӵ��ø��๹�������г�ʼ��
            super(name);
        }
        program() {
            console.log("I'm coding...");
        }
    }
    
    // �������ǵ���
    var animal = new Animal('dummy'),
        wayou = new Programmer('wayou');
    animal.sayName(); // ��� 'My name is dummy'
    wayou.sayName(); // ��� 'My name is wayou'
    wayou.program(); // ��� 'I'm coding...'
 
##��ǿ�Ķ���������

��������������ǿ�ˣ�д�����Ӽ������ͬʱ�ڶ�������ʱ���ܹ�������������ˡ���������ڣ�

1. �����ڶ������������涨��ԭ��
2. ���巽�����Բ���function�ؼ���
3. ֱ�ӵ��ø��෽��

����һ����������������ǰ���ᵽ�����������Ǻϣ��ڱ�д��������JavaScriptʱ�������ɷ����ˡ�

    // ͨ��������������������
    var human = { 
        breathe() {
            console.log('breathing...');
        }
    };
    
    var worker = { 
        __proto__: human, // ���ô˶����ԭ��Ϊhuman, �൱�ڼ̳�human
        company: 'freelancer',
        work() {
            console.log('working...');
        }
    };
    
    human.breathe(); // ��� 'breathing...'
    
    // ���ü̳�����breathe����
    worker.breathe(); // ��� 'breathing...'
 
##�ַ���ģ��

�ַ���ģ����Լ��׶�Щ��ES6������ʹ�÷����� \` �������ַ��������ַ����������ַ���������԰�������Ԫ���żӻ����Ű����ı��� `${vraible}`�������ʹ�ù���C#�Ⱥ��ǿ�������ԵĻ����Դ˹���Ӧ�ò���İ����

    // ����һ�������
    var num = Math.random();
    
    // ��������������console 
    console.log(`your num is ${num}`);

##�⹹

�Զ��������������е�ֵ��������һ������Ҫ���ض��ֵ������������Ƿ���һ�����󣬽�ÿ��ֵ��Ϊ�����������Է��ء�����ES6�У����ý⹹��һ���ԣ�����ֱ�ӷ���һ�����飬Ȼ�������е�ֵ���Զ�����������Ӧ���ո�ֵ�ı����С�

    function getVal() {
        return[1,2];
    }
    var [x,y] = getVal(), // ��������ֵ�Ľ⹹
    console.log('x:' + x + ', y:' + y); // �����x:1, y:2
    
    [name,,age] = ['wayou','male','secrect']; // ����⹹
    console.log('name:' + name + ', age:' + age); //�����name:wayou, age:secrect 

##����Ĭ��ֵ��������������չ����

###Ĭ�ϲ���ֵ

���ڿ����ڶ��庯����ʱ��ָ��������Ĭ��ֵ�ˣ�����������ǰ����ͨ���߼�����������ﵽĿ���ˡ�

    function sayHello(name) {
        // ��ͳ��ָ��Ĭ�ϲ����ķ�ʽ
        var name = name || 'dude';
        console.log('Hello ' + name);
    }  
    sayHello(); // �����Hello dude
    sayHello('Wayou'); // �����Hello Wayou
    
    // ����ES6��Ĭ�ϲ���
    function sayHello2(name = 'dude') {
        console.log(`Hello${name}`);
    }
    sayHello2(); // �����Hello dude
    sayHello2('Wayou'); // �����Hello Wayou
 
###��������

�����������ں�����ʹ����������ͬʱ���ղ���������δ������������ֻ��һ���﷨�ǣ�����ǰ��JavaScript���������ǿ���ͨ��arguments�������ﵽ��һĿ�ġ����������ĸ�ʽ������������������в��������ı�������

����������������У���x���������д���add�����Ĳ�����

    // �����в�����ӵĺ���
    function add(...x) {
        return x.reduce((m,n) => m+n);
    }
    
    // ������������Ĳ���
    console.log(add(1,2,3)); // �����6
    console.log(add(1,2,3,4,5)); // �����15
 
###��չ����

��չ����������һ����ʽ���﷨�ǣ����������������������ֱ����Ϊ�����Ĳ���������ͨ��apply��

    var people = ['Wayou','John','Sherlock'];
    
    // sayHello���������������������Ĳ�����һ���˶�������
    function sayHello(people1, people2, people3) {
        console.log(`Hello${people1}, ${people2}, ${people3}`);
    }
    
    // �������ǽ�һ����������չ��������ʽ���ݣ����ܺܺõ�ӳ�䵽ÿ�������Ĳ���
    sayHello(...people); // �����Hello Wayou,John,Sherlock
    
    // ������ǰ�������Ҫ�������鵱������������Ҫʹ�ú�����apply����
    sayHello.apply(null, people); // �����Hello Wayou,John,Sherlock 

##let��const �ؼ���

���԰�let����var��ֻ��������ı������޶������ض���Χ�ڲ���ʹ�ã����뿪�����Χ����Ч��const���ֱ�ۣ��������峣�������޷�������ֵ�ı�����

    for (let i=0; i<2; i++) {
        console.log(i); // ���: 0,1
    }
    console.log(i); // �����undefined,�ϸ�ģʽ�»ᱨ��

##for of ֵ����

���Ƕ�֪��for inѭ�����ڱ������飬����������ES6���������for ofѭ���������ƣ���ͬ����ÿ��ѭ�����ṩ�Ĳ�����Ŷ���ֵ��

    var someArray = ["a","b","c"];
    for (v of someArray) {
        console.log(v); // ��� a,b,c
    }

##iterator, generator

1. iterator: ������ôһ������ӵ��һ��next�����������������һ������{done,value}�������������������ԣ�һ���������͵�done�Ͱ�������ֵ��value
 
2. iterable: ������ôһ������ӵ��һ��obj[@@iterator]�����������������һ��iterator
 
3. generator: ����һ�������iterator������next�������Խ���һ���������ҷ���ֵȡ�������Ĺ��캯����generator function����generatorͬʱӵ��һ��throw����
 
4. generator����: ��generator�Ĺ��캯�����˺����ڿ���ʹ��yield�ؼ��֡���yield���ֵĵط�����ͨ��generator��next��throw��������紫��ֵ��generator ������ͨ��function*��������
 
5. yield�ؼ��֣���������ͣ������ִ�У��������ٽ����뺯������ִ��

##ģ��

��ES6��׼�У�JavaScriptԭ��֧��module�ˡ����ֽ�JS����ָ�ɲ�ͬ���ܵ�С�����ģ�黯�ĸ�������һЩ�����淶�����������ģ�����CommonJS��AMDģʽ��

����ͬ���ܵĴ���ֱ�д�ڲ�ͬ�ļ��У���ģ��ֻ�赼�������ӿڲ��֣�Ȼ��ͨ��ģ��ĵ���ķ�ʽ�����������ط�ʹ�á�

    // point.js
    module "point" {
        export class Point {
            constructor(x,y) {
                public x=x;
                public y=y;
            }
        }
    }
    
    // myapp.js
    
    // �������õ�ģ�� 
    module point from "/point.js";
    
    // ������Կ������������������õ�ģ�飬���ǿ���ͨ��ָ����Ҫ�Ĳ��ֽ��е���
    import Point from "point";
    var origin = new Point(0,0);
    console.log(origin);

##Map��Set �� WeakMap��WeakSet

��Щ���¼ӵļ������ͣ��ṩ�˸��ӷ���Ļ�ȡ����ֵ�ķ�������������ǰһ����hasOwnProperty�����ĳ������������ԭ�����ϵ��ػ��ǵ�ǰ����ġ�ͬʱ���ڽ�������ֵ������ȡʱ��ר�ŵ�get��set������

    // Sets 
    var s = new Set();
    s.add("hello").add("goodbye");
    s.size === 2;
    s.has("hello") === true;
    
    // Maps
    var m = new Map();
    m.set("hello", 42);
    m.set(s, 34);
    m.get(s) == 34;

��ʱ�����ǻ�Ѷ�����Ϊһ������ļ������������ֵ����ͨ�������ͱ���򵥶������ֹ��������������Щ��Ϊ���Լ����ڵĶ���Ļ��գ�������ڴ�й©��Σ�ա���WeakMap,WeakSet����Ӱ�ȫЩ����Щ��Ϊ���Լ��Ķ������û�б�ı������������ǣ���ᱻ�����ͷŵ������廹����������ӣ�

    // Weak Maps
    var wm = new WeakMap();
    wm.set(s, {extra: 42});
    wm.size === undefined // �����ͷ���
    
    // Weak Sets
    var ws = new WeakSet();
    ws.add({data: 42}); // ��Ϊ��ӵ�ws�������ʱ����û����������������������ws���ᱣ������ֵ��Ҳ����˵��������ʵû����˼
 
##Proxies

Proxy���Լ����������Ϸ�����ʲô���飬������Щ���鷢����ִ��һЩ��Ӧ�Ĳ�����һ���������Ƕ�һ���������˺�ǿ��׷��������ͬʱ�����ݰ󶨷���Ҳ�����ô���

    // ���屻������Ŀ�����
    var engineer = {name: 'Joe Sixpack', salary: 50};
    
    // ���崦�����
    var interceptor = {set: function(receiver, property, value) {
        console.log(property, 'is changed to', value);
        receiver[property] = value;
        }
    };
    
    // ���������Խ�������
    engineer = Proxy(engineer, interceptor);
    
    //��һЩ�Ķ�����������
    engineer.salary = 60; // ����̨�����salary is changed to 60

����������Ѽ���ע�ͣ������һ�����͡����ڴ���������ڱ������Ķ������Ϸ�������Ӧ�¼�֮�󣬴����������ķ����ͻᱻ���ã���������������������set�Ĵ�������������������������Ķ�������Ա����ģ�Ҳ���Ǳ�set�ˣ�������������ͻᱻ���ã�ͬʱͨ�������ܹ���֪���ĸ����Ա����ģ�����Ϊ��ʲôֵ��

##Symbols

����֪��������ʵ�Ǽ�ֵ�Եļ��ϣ�����ͨ����˵���ַ����������ڳ����ַ����⣬���ǻ�������symbol����ֵ����Ϊ����ļ���Symbol��һ�� �������ͣ������֣��ַ������в���һ����������һ������Symbol ͨ������symbol����������������һ����ѡ�����ֲ������ú������ص�symbol��Ψһ�ġ�֮��Ϳ������������ֵ��Ϊ����ļ��ˡ�Symbol��������������˽�����ԣ��ⲿ�޷�ֱ�ӷ�����symbol��Ϊ��������ֵ��

    (function() {
        // ���� symbol
        var key = Symbol("key");
        function MyClass(privateData) {
            this[key] = privateData;
        }
        MyClass.prototype = {
            doStuff: function() {
                ...this[key]...
            }
        };
    })();
    var c = new MyClass("hello");
    c["key"] === undefined //�޷����ʸ����ԣ���Ϊ��˽�е�
 
##Math��Number��String��Object ����API

��Math,Number,String����Object�����������µ�API��

    // Number
    // ��ͬ������Number֮�����С�Ĳ�
    Number.EPSILON
    
    // �ж��Ƿ�������
    Number.isInteger(Infinity) // false
    
    // �ж��Ƿ�Ϊ������
    Number.isNaN("NaN") // false
    
    // Math
    Math.acosh(3) // 1.762747174039086
    Math.hypot(3,4) // 5
    Math.imul(Math.pow(2,32)-1, Math.pow(2,32)-2) // 2
    
    // String
    "abcde".contains("cd") // true
    "abc".repeat(3) // "abcabcabc"
    
    // Array
    // ��һ������������ɵ�������ת������ʵ������
    Array.from(document.querySelectorAll('*'))
    
    // �������������͵Ķ����������һ�������ﲢ����
    Array.of(1,2,3)
    
    // ��һ��������ָ�����������Ԫ�ص�ֵ, ���滻�ɻ���˵����Ϊĳ���̶���ֵ
    [0,0,0].fill(7,1) // [0,7,7]
    
    // ��������������ĳָ��Ԫ�ص�����, ����Ҳ���ָ����Ԫ��, �򷵻� -1
    [1,2,3].findIndex(x => x == 2) // 1
    
    // ����һ�� Array Iterator ���󣬸ö������������ÿһ�������ļ�ֵ��
    ["a","b","c"].entries() // iterator [0, "a"], [1,"b"], [2,"c"]
    
    // ����һ�����������ĵ�����
    ["a","b","c"].keys() // iterator 0, 1, 2
    
    // ����һ���µ� Array Iterator ���󣬸ö����������ÿ��������ֵ
    ["a","b","c"].values() // iterator "a", "b", "c"
    
    // Object
    Object.assign(Point, {origin: new Point(0,0)})
 
##Promises

Promises�Ǵ����첽������һ��ģʽ��֮ǰ�ںܶ�����������ʵ�֣�����jQuery��deferred ���󡣵��㷢��һ���첽���󣬲�����.when(), .done()���¼��������ʱ����ʵ������Ӧ��promiseģʽ��

    // ���� promise
    var promise = new Promise(function(resolve,reject) {
        // ����һЩ�첽���ʱ����
        if(/*����ɹ� */) {
            resolve("Stuff worked!");
        } else {
            reject(Error("It broke"));
        }
    });
    
    // �󶨴������
    promise.then(function(result) {
        // promise�ɹ��Ļ���ִ������
        console.log(result); // "Stuff worked!"
    }, function(err) {
        // promiseʧ�ܻ�ִ������
        console.log(err); // Error: "It broke"
    });

##����

1. �����ES6���붼�������������ת����[ES6תES5](http://google.github.io/traceur-compiler/demo/repl.html)
2. ��һ����ʦ��[ECMAScript 6����](http://es6.ruanyifeng.com/#README)
3. ����ϸ�Ľ��ܣ�������[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)