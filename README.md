# PhotoMaster
### これだけは抑えておくポイント  <br>

### Swiftの⾔語特性  <br>
「カメラ」ボタンを押した時に呼ばれるメソッド
```swift
@IBAction func onTappedCameraButton() {
        presentPickerController(sourceType: .camera)
    }
```
「アルバム」ボタンを押したときに呼ばれるメソッド
```swift
@IBAction func onTappedAlbumButtom() {
        presentPickerController(sourceType: .photoLibrary)

    }
```

カメラとアルバムの呼び出しメソッド
```swift
func presentPickerController(sourceType: UIImagePickerController.SourceType) {
        if UIImagePickerController.isSourceTypeAvailable(sourceType) {
            let picker = UIImagePickerController()
            picker.sourceType = sourceType
            picker.delegate = self
            
            self.present(picker, animated: true, completion: nil)
        }
    }
```
写真が選択された時に呼ばれるメソッド
```swift
func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info:[UIImagePickerController.InfoKey: Any]){
        self.dismiss(animated: true, completion: nil)
        //画像を出力
        photoImageView.image = info[.originalImage] as? UIImage
    }
```    

### エラーが起きたところ・起きそうなところ <br>
コードを書いて関連づけただけではアプリが落ちてしまう。

### 原因  <br>
iOS10以降のプライバシー規約が変更されたため、ユーザにカメラロール、カメラの許可を求めなくてはいけない

### 解決⽅法
1. info.plistを選択  <br>
2. 何もないところで右クリックをしてAdd Rowを選択する
3. Add rowで各許可を求めるよう設定する
