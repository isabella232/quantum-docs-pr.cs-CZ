---
uid: Microsoft.Quantum.Canon.IsResultZero
title: IsResultZero – funkce
ms.date: 11/25/2020 12:00:00 AM
ms.topic: article
qsharp.kind: function
qsharp.namespace: Microsoft.Quantum.Canon
qsharp.name: IsResultZero
qsharp.summary: Tests if a given Result value is equal to `Zero`.
ms.openlocfilehash: b4e9b62b20e12a8dce544ce16dcddcf15fdf2680
ms.sourcegitcommit: a87c1aa8e7453360025e47ba614f25b02ea84ec3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/26/2020
ms.locfileid: "96206523"
---
# <a name="isresultzero-function"></a>IsResultZero – funkce

Obor názvů: [Microsoft.. Canon](xref:Microsoft.Quantum.Canon)

Balíček: [Microsoft.. Standard](https://nuget.org/packages/Microsoft.Quantum.Standard)


Testuje, zda je daná hodnota výsledku rovna `Zero` .

```qsharp
function IsResultZero (input : Result) : Bool
```


## <a name="input"></a>Vstup

### <a name="input--__invalidresult__"></a>vstup: __neplatné <Result>__

`Result` hodnota, která má být testována.



## <a name="output--bool"></a>Výstup: [bool](xref:microsoft.quantum.lang-ref.bool)

Vrátí, `true` Pokud `input` je rovno `Zero` .