---
uid: Microsoft.Quantum.Characterization.EstimateImagOverlapBetweenStates
title: Operace EstimateImagOverlapBetweenStates
ms.date: 10/26/2020 12:00:00 AM
ms.topic: article
qsharp.kind: operation
qsharp.namespace: Microsoft.Quantum.Characterization
qsharp.name: EstimateImagOverlapBetweenStates
qsharp.summary: Given two operations which each prepare copies of a state, estimates the imaginary part of the overlap between the states prepared by each operation.
ms.openlocfilehash: 8b73115c3243c594897ac4b309ec52d5e9863d26
ms.sourcegitcommit: 29e0d88a30e4166fa580132124b0eb57e1f0e986
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/27/2020
ms.locfileid: "92698744"
---
# <a name="estimateimagoverlapbetweenstates-operation"></a>Operace EstimateImagOverlapBetweenStates

Obor názvů: [Microsoft.. Popis](xref:Microsoft.Quantum.Characterization)

Balíček [](https://nuget.org/packages/)


Vzhledem k tomu, že jednotlivé operace připravují kopie stavu, odhadne imaginární část překrytí mezi stavy, které jsou připraveny jednotlivými operacemi.

```qsharp
operation EstimateImagOverlapBetweenStates (commonPreparation : (Qubit[] => Unit is Adj), preparation1 : (Qubit[] => Unit is Adj + Ctl), preparation2 : (Qubit[] => Unit is Adj + Ctl), nQubits : Int, nMeasurements : Int) : Double
```


## <a name="input"></a>Vstup

### <a name="commonpreparation--qubit--unit-adj"></a>commonPreparation: [qubit](xref:microsoft.quantum.lang-ref.qubit)[] => [jednotky](xref:microsoft.quantum.lang-ref.unit) ADJ

Operace, která připraví pevný vstupní stav.


### <a name="preparation1--qubit--unit-adj--ctl"></a>preparation1: [qubit](xref:microsoft.quantum.lang-ref.qubit)[] => [jednotky](xref:microsoft.quantum.lang-ref.unit) ADJ + CTL

První z těchto dvou operací přípravy stavu, které mají být porovnány.


### <a name="preparation2--qubit--unit-adj--ctl"></a>preparation2: [qubit](xref:microsoft.quantum.lang-ref.qubit)[] => [jednotky](xref:microsoft.quantum.lang-ref.unit) ADJ + CTL

Druhý ze dvou operací přípravení stavu, které mají být porovnány.


### <a name="nqubits--int"></a>nQubits: [int](xref:microsoft.quantum.lang-ref.int)

Počet qubits, které jsou `commonPreparation` , `preparation1` a `preparation2` všechny Act.


### <a name="nmeasurements--int"></a>nMeasurements: [int](xref:microsoft.quantum.lang-ref.int)

Počet měření, která se mají použít při odhadování překrytí



## <a name="output--double"></a>Výstup: [Double](xref:microsoft.quantum.lang-ref.double)



## <a name="remarks"></a>Poznámky

Tato operace používá test Hadamard k vyhledání imaginární části pro $ $ \begin{align} \braket{\psi | V ^ {\dagger} U | \psi} \end{align} $ $ kde $ \ket{\psi} $ je stav, který připravil `commonPreparation` , $U $ je jednotková reprezentace akce `preparation1` a kde $V $ odpovídá `preparation2` .

## <a name="references"></a>Odkazy

- Aharonov *et al.* [quant-pH/0511096](https://arxiv.org/abs/quant-ph/0511096).

## <a name="see-also"></a>Viz také

- [Microsoft. proEstimateRealOverlapBetweenStates. Popis.](xref:Microsoft.Quantum.Characterization.EstimateRealOverlapBetweenStates)
- [Microsoft. proEstimateOverlapBetweenStates. Popis.](xref:Microsoft.Quantum.Characterization.EstimateOverlapBetweenStates)