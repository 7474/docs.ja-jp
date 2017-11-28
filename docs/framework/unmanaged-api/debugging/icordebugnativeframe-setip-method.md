---
title: "ICorDebugNativeFrame::SetIP メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugNativeFrame.SetIP
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugNativeFrame::SetIP
helpviewer_keywords:
- ICorDebugNativeFrame::SetIP method [.NET Framework debugging]
- SetIP method, ICorDebugNativeFrame interface [.NET Framework debugging]
ms.assetid: 57784a51-c76d-48f8-9392-584d0e1946d9
topic_type: apiref
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 563566a877d589ecd32575c095cdc812c28f6334
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugnativeframesetip-method"></a><span data-ttu-id="99e1e-102">ICorDebugNativeFrame::SetIP メソッド</span><span class="sxs-lookup"><span data-stu-id="99e1e-102">ICorDebugNativeFrame::SetIP Method</span></span>
<span data-ttu-id="99e1e-103">命令ポインターをネイティブ コードで指定されたオフセット位置に設定します。</span><span class="sxs-lookup"><span data-stu-id="99e1e-103">Sets the instruction pointer to the specified offset location in native code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="99e1e-104">構文</span><span class="sxs-lookup"><span data-stu-id="99e1e-104">Syntax</span></span>  
  
```  
HRESULT SetIP (  
    [in] ULONG32 nOffset  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="99e1e-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="99e1e-105">Parameters</span></span>  
 `nOffset`  
 <span data-ttu-id="99e1e-106">[in]ネイティブ コード内のオフセットの位置。</span><span class="sxs-lookup"><span data-stu-id="99e1e-106">[in] The offset location in the native code.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="99e1e-107">コメント</span><span class="sxs-lookup"><span data-stu-id="99e1e-107">Remarks</span></span>  
 <span data-ttu-id="99e1e-108">呼び出す`SetIP`すぐにすべてのフレームと現在のスレッドのチェーンが無効にします。</span><span class="sxs-lookup"><span data-stu-id="99e1e-108">Calls to `SetIP` immediately invalidate all frames and chains for the current thread.</span></span> <span data-ttu-id="99e1e-109">デバッガーには、呼び出しの後にフレーム情報が必要がある場合`SetIP`、新しいスタック トレースを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="99e1e-109">If the debugger needs frame information after a call to `SetIP`, it must perform a new stack trace.</span></span>  
  
 <span data-ttu-id="99e1e-110">[ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)に有効な状態でスタック フレームを維持しようとします。</span><span class="sxs-lookup"><span data-stu-id="99e1e-110">[ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) will attempt to keep the stack frame in a valid state.</span></span> <span data-ttu-id="99e1e-111">ただし、場合でも、限り、ランタイムは、有効な状態では、フレームは、まだある可能性があります初期化されていないローカル変数などの問題です。</span><span class="sxs-lookup"><span data-stu-id="99e1e-111">However, even if the frame is in a valid state, as far as the runtime is concerned, there still may be problems, such as uninitialized local variables, and so on.</span></span> <span data-ttu-id="99e1e-112">呼び出し元は、実行中のプログラムの一貫性を保証します。</span><span class="sxs-lookup"><span data-stu-id="99e1e-112">The caller is responsible for insuring coherency of the running program.</span></span>  
  
 <span data-ttu-id="99e1e-113">64 ビット プラットフォームでは、上の命令ポインターを移動できません、`catch`または`finally`ブロックします。</span><span class="sxs-lookup"><span data-stu-id="99e1e-113">On 64-bit platforms, the instruction pointer cannot be moved out of a `catch` or `finally` block.</span></span> <span data-ttu-id="99e1e-114">場合`SetIP`が呼び出された 64 ビット プラットフォームで、このような移動をするためには、エラーを示す HRESULT を返します。</span><span class="sxs-lookup"><span data-stu-id="99e1e-114">If `SetIP` is called to make such a move on a 64-bit platform, it will return an HRESULT indicating failure.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="99e1e-115">要件</span><span class="sxs-lookup"><span data-stu-id="99e1e-115">Requirements</span></span>  
 <span data-ttu-id="99e1e-116">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="99e1e-116">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="99e1e-117">**ヘッダー:** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="99e1e-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="99e1e-118">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="99e1e-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="99e1e-119">**.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="99e1e-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="99e1e-120">関連項目</span><span class="sxs-lookup"><span data-stu-id="99e1e-120">See Also</span></span>  
 