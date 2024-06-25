# VRMRuntimeImportPlugin

VRMファイルをゲーム実行時に読み込んで、簡単に操作可能なキャラクターとして使用するためのプラグイン。  
使用するには、[VRM4Uプラグイン](https://ruyo.github.io/VRM4U/01_quick-start/)が別途必要です。  
また、アニメーションをサードパーソンテンプレートのマネキンのものを流用することができますが、その際はサードパーソンテンプレートの一部ファイルが必要です。

VRMRuntimeImportPluginには以下のアセットが含まれています。
- VRMファイルの読み込み用
  - LoadVRMFileAsyncMacroLibrary
  - SkeletaMeshInjectorByVRM

- リターゲット用
  - IK_VRoidSimple

- サードパーソンテンプレートからのリターゲット用
  - RTG_Mannequin_VRoidSimple
  - ABP_RTG_Mannequin_VRoidSimple

## LoadVRMFileAsyncMacroLibrary
ファイルパスと、インポートオプションを指定すると、指定したパスにあるVRMファイルをロードします。

## SkeletalMeshInjectorByVRM
キャラクターのスケルタルメッシュを、インポートしたスケルタルメッシュに変更するためのクラスです。  
"Construct Object From Class" ノードでインスタンスを作成してから使用します。  
以下の手順で操作キャラクターをインポートしたメッシュに変更できます。
1. Initialize 関数で変更適用先のスケルタルメッシュを指定して初期化
2. PossessSkeletalMeshComponent 関数で変更適用先のスケルタルメッシュを、インポートしたスケルタルメッシュに変更  
   Anim Instance Class には、Retarget Pose From Mesh でリターゲティングするようなアニメーションブループリントを指定すること。  
   その際、指定するIKRetargeterは、Target IKRig Assset を IK_VRoidSimple にすること。

なお、実際は変更適用先のスケルタルメッシュのメッシュを変更しているのではなく、非表示にして、子コンポーネントにVRM用のスケルタルメッシュを追加しています。  
アニメーションをリターゲティングするには、元の動いているスケルタルメッシュを残しておかないと動作しないので、このように実装しています。
