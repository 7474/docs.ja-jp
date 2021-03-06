---
title: virtualCERCall MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), CER calls
- virtualCERCall MDA
- virtual CER calls
- constrained execution regions
- CER calls
- managed debugging assistants (MDAs), CER calls
ms.assetid: 1eb18c7a-f5e0-443f-80fb-67bfbb047da2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c2f2104768144da244679e5d0be884d70a3ba6b0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33386653"
---
# <a name="virtualcercall-mda"></a>virtualCERCall MDA
`virtualCERCall` マネージ デバッグ アシスタント (MDA) は、制約された実行領域 (CER) 呼び出し先の呼び出しサイトが、仮想ターゲット (つまり、インターフェイスを使用した最終ではない仮想メソッドまたは呼び出しの仮想呼び出し) を参照していることを示す警告としてアクティブ化されます。 共通言語ランタイム (CLR) は、中間言語およびメタデータの分析だけでは、これらの呼び出しの呼び出し先メソッドを予測できません。 その結果、CER グラフの一部としてコール ツリーを準備できません。また、そのサブツリー内のスレッドの中止を自動的にブロックできません。 呼び出し対象の計算に必要な追加情報が実行時に判明すると、<xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> メソッドの明示的な呼び出しを使用して CER の拡張が必要な可能性がある場合に、この MDA は警告します。  
  
## <a name="symptoms"></a>現象  
 スレッドが中止されたとき、またはアプリケーション ドメインがアンロードされたときに CER が実行されません。  
  
## <a name="cause"></a>原因  
 CER に、自動的に準備できない仮想メソッドの呼び出しが含まれています。  
  
## <a name="resolution"></a>解像度  
 仮想メソッドの <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> を呼び出します。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 この MDA は CLR に影響しません。  
  
## <a name="output"></a>出力  
  
```  
Method 'MethodWithCer', while executing within a constrained execution region, makes a call  
at IL offset 0x0024 to 'VirtualMethod', which is virtual and cannot be prepared automatically  
at compile time. The caller must ensure this method is prepared explicitly at  
runtime before entering the constrained execution region.  
method name="VirtualMethod"  
declaringType name="VirtualCERCall+MyClass"  
  declaringModule name="mda"  
    callsite name="MethodWithCer" offset="0x0024"  
```  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    < VirtualCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>例  
  
```  
class MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    virtual void VirtualMethod()  
    {  
        ...  
    }  
}  
  
class MyDerivedClass : MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    override void VirtualMethod()  
    {  
        ...  
    }  
}  
  
void MethodWithCer(MyClass object)  
{  
    RuntimeHelpers.PrepareConstrainedRegions();  
    try  
    {  
        ...  
    }  
    finally  
    {  
        // Start of the CER.  
  
        // Cannot tell at analysis time whether object is a MyClass  
        // or a MyDerivedClass, so we do not know which version of   
        // VirtualMethod we are going to call.  
        object.VirtualMethod();  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>  
 [マネージ デバッグ アシスタントによるエラーの診断](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)  
 [相互運用マーシャリング](../../../docs/framework/interop/interop-marshaling.md)
