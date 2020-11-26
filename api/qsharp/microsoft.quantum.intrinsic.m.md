---
uid: Microsoft.Quantum.Intrinsic.M
title: M operace
ms.date: 10/26/2020 12:00:00 AM
ms.topic: article
qsharp.kind: operation
qsharp.namespace: Microsoft.Quantum.Intrinsic
qsharp.name: M
qsharp.summary: >-
  Performs a measurement of a single qubit in the Pauli $Z$ basis.

  The output result is given by the distribution \begin{align} \Pr(\texttt{Zero} | \ket{\psi}) = \braket{\psi | 0} \braket{0 | \psi}. \end{align}
ms.openlocfilehash: 8d4b120385bfc7086a7cb0e3f77034c760d78d92
ms.sourcegitcommit: 29e0d88a30e4166fa580132124b0eb57e1f0e986
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/27/2020
ms.locfileid: "92707153"
---
# <a name="m-operation"></a>M operace

Obor názvů: [Microsoft.. vnitřní](xref:Microsoft.Quantum.Intrinsic)

Balíček [](https://nuget.org/packages/)


Provede měření jediného qubitu v Pauli $Z $.

Výsledek výstupu je dán distribucí \begin{align} \Pr (\texttt{Zero} | \ket{\psi}) = \braket{\psi | 0} \braket{0 | \psi}.
\end{align}

```qsharp
operation M (qubit : Qubit) : Result
```


## <a name="input"></a>Vstup

### <a name="qubit--qubit"></a>qubit: [qubit](xref:microsoft.quantum.lang-ref.qubit)

Qubit k měření.



## <a name="output--__invalidresult__"></a>Výstup: __neplatný <Result>__

`Zero` Pokud se eigenvalue $ + $1, a `One` Pokud je zjištěna $-$1 eigenvalue.

## <a name="remarks"></a>Poznámky

Ekvivalent:

```qsharp
Measure([PauliZ], [qubit]);
```