title: Add UITextField on UIView Programmitically by Swift
date: 2015-07-17 11:44:40
categories:
- Tech
- iOS
tags:
- iOS
- UI
- Swift
---

好像有點久沒有寫文章。。。

最近開始玩 iOS SDK，今天不知道哪根筋不對，突然不想用 Interface Builder 拉 UI，想直接用寫 Code 的方式生，所以我就翻了一下關方手冊，還有拜了 Google 大神！萬事起頭難，我們就先從簡單的開始吧，以下是我找到的方法，請參考！

### 最簡單的作法
從官方手冊上看到最簡單的辦法就是直接呼叫 UITextField(frame:) 這個建構式，但這個建構式必須傳入一個 CGRect 型別的 frame 變數，到這個 frame 要怎麼建立勒？官方提供了 [CGRectMake(x, y, width, height)](https://developer.apple.com/library/prerelease/ios/documentation/GraphicsImaging/Reference/CGGeometry/index.html#//apple_ref/c/func/CGRectMake) 這個方法可以快速的產生 UITextField 需要的 frame，說簡單一點就是透過 CGRectMake() 告訴 iOS 這個 UITextField 的外框多大、位置在哪，最後透過 addSubview() 這個方法將 UITextField 放到 view 上面。 
```Swift
//產生 UITextField 元件
var txtField = UITextField(frame: CGRectMake(10, 200, 300, 30));

//放到 view 上面
self.view.addSubview(txtField);
```

### 進階的作法
透過上述的方式可以快速產生一個白白的 UITextField，但如果想產生像 Interface Builder 拉出來的，要怎麼做？除了上面那兩行外，還做一些額外的設定，這樣 UITextField 就可以像 iOS 預設的一樣簡單又漂亮！以下是我的做法：
```Swift
var txtField = UITextField(frame: CGRectMake(10, 200, 300, 30));
txtField.borderStyle = UITextBorderStyle.RoundedRect;
txtField.font = UIFont.systemFontOfSize(15);
txtField.placeholder = "Select Drawing";
txtField.autocorrectionType = UITextAutocorrectionType.No;
txtField.keyboardType = UIKeyboardType.Default;
txtField.returnKeyType = UIReturnKeyType.Done;
txtField.clearButtonMode = UITextFieldViewMode.WhileEditing;
txtField.contentVerticalAlignment = UIControlContentVerticalAlignment.Center;

self.view.addSubview(txtField);
```

Ref. [View Programming Guilde for iOS](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingViews/CreatingViews.html#//apple_ref/doc/uid/TP40009503-CH5-SW1)
