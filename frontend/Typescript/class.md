class用于定义一个类，可以包含属性、方法和构造函数等成员，类是ts的核心语言特性之一，可以帮助开发者很好的组织代码，提高代码的可读性和可维护性。

```ts
class Animal {
    public name: string;
    private gender: string;
    protected height: number; // 身高
    constructor(name: string, height: number, gender?: string) {
        this.name = name;
        this.gender = gender || "";
        this.height = height;
    }
    public move(distance: number = 0) {
        console.log(`身高${this.height}的${this.name}移动了${distance}米!`);
    }

    public getBasicInfo(){
        return {
            name: this.name,
            height: this.height,
            gender: this.gender
        };
    }
}

class Dog extends Animal {
    constructor(name: string, height: number, gender?: string) {
        super(name, height, gender);
    }
    bark() {
        console.log(`身高位${this.height}厘米的${this.name}汪汪叫!`); // 身高位88厘米的Buddy汪汪叫!子类中访问到了父类中的受保护成员height
    }
}

const dog = new Dog("Buddy", 88, "男");
dog.bark(); // 汪汪叫
dog.move(20); // Buddy移动了20米!
console.log(dog.getBasicInfo());
```

#### 成员访问修饰符

上面的案例中，我们看到了private，这是一个成员访问修饰符，除了private之外，还有另外的几个访问修饰符如public、protected。

public:表示该成员可以在类的内部和外部都能被访问；

private: 表示该成员只能在类的内部被访问；

protected:表示该成员只能在类的内部和派生类中被访问；

子类可以访问父类中的受保护成员，包括属性和方法，但是只能是在子类的实例方法中或者子类的构造函数中才能访问父类中的受保护成员。

```ts
class Dog extends Animal {
    bark() {
        console.log(`身高位${this.height}厘米的${this.name}汪汪叫!`); // 身高位88厘米的Buddy汪汪叫!子类中访问到了父类中的受保护成员height
    }
}
```

> 子类的实例不能直接访问父类中的受保护成员，只能通过子类的实例方法或者子类的构造函数去访问父类中的受保护成员。