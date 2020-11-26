---
uid: Microsoft.Quantum.Oracles.ReflectionOracle
title: Uživatelem definovaný typ ReflectionOracle
ms.date: 10/26/2020 12:00:00 AM
ms.topic: article
qsharp.kind: udt
qsharp.namespace: Microsoft.Quantum.Oracles
qsharp.name: ReflectionOracle
qsharp.summary: >-
  Represents a reflection oracle.

  A reflection oracle, $O$, has inputs:

  - The phase $\phi$ by which to rotate the reflected subspace. - The qubit register on which to perform the given reflection.
ms.openlocfilehash: 8e35e7e508ea7e0c30ea2a70633f71a6c87d4be1
ms.sourcegitcommit: 29e0d88a30e4166fa580132124b0eb57e1f0e986
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/27/2020
ms.locfileid: "92708740"
---
# <a name="reflectionoracle-user-defined-type"></a>Uživatelem definovaný typ ReflectionOracle

Obor názvů: [Microsoft.... Oracle](xref:Microsoft.Quantum.Oracles)

Balíček [](https://nuget.org/packages/)


Představuje reflexi Oracle.

Reflexe Oracle, $O $, má vstupy:

- Fáze $ \phi $, o kterou se má otočit odrážet mezera.
- Registr qubit, na kterém se má provést daná reflexe.

```qsharp

newtype ReflectionOracle = (ApplyReflection : ((Double, Qubit[]) => Unit is Adj + Ctl));
```



## <a name="named-items"></a>Pojmenované položky

### <a name="applyreflection--doublequbit--unit-adj--ctl"></a>ApplyReflection: ([Double](xref:microsoft.quantum.lang-ref.double),[qubit](xref:microsoft.quantum.lang-ref.qubit)[]) => [jednotka](xref:microsoft.quantum.lang-ref.unit) ADJ + CTL



## <a name="remarks"></a>Poznámky

Tento Oracle $O = \boldone-(1-e ^ {i \phi}) \ket{\psi}\bra{\psi} $ provede částečný odraz pomocí fáze $ \phi $ o jednom čistě stavu $ \ket{\psi} $.