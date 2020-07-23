---
title: 'Použití dalších knihoven Q #'
description: 'Přečtěte si, jak přidat další knihovny Q # do aplikací pro vlastníce.'
author: cgranade
ms.author: chgranad
ms.date: 06/30/2020
ms.topic: article
uid: microsoft.quantum.libraries.using
ms.openlocfilehash: b82113b925870d07c8a28aecd50176e009826062
ms.sourcegitcommit: cdf67362d7b157254e6fe5c63a1c5551183fc589
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/21/2020
ms.locfileid: "86872612"
---
# <a name="using-additional-q-libraries"></a><span data-ttu-id="2bf26-103">Použití dalších knihoven Q #</span><span class="sxs-lookup"><span data-stu-id="2bf26-103">Using Additional Q# Libraries</span></span>

<span data-ttu-id="2bf26-104">Sada pro vývoj z více procesorů poskytuje další funkce specifické pro doménu prostřednictvím _balíčků NuGet_ , které je možné přidat do projektů Q #.</span><span class="sxs-lookup"><span data-stu-id="2bf26-104">The Quantum Development Kit provides additional domain-specific functionality through _NuGet packages_ that can be added to your Q# projects.</span></span>

| <span data-ttu-id="2bf26-105">Knihovna Q #</span><span class="sxs-lookup"><span data-stu-id="2bf26-105">Q# Library</span></span>  | <span data-ttu-id="2bf26-106">Balíček NuGet</span><span class="sxs-lookup"><span data-stu-id="2bf26-106">NuGet package</span></span> | <span data-ttu-id="2bf26-107">Poznámky</span><span class="sxs-lookup"><span data-stu-id="2bf26-107">Notes</span></span> |
|---------|---------|--------|
| [<span data-ttu-id="2bf26-108">Q # standardní knihovna</span><span class="sxs-lookup"><span data-stu-id="2bf26-108">Q# standard library</span></span>](xref:microsoft.quantum.libraries.standard.intro) | [<span data-ttu-id="2bf26-109">**Microsoft. nestandardní**</span><span class="sxs-lookup"><span data-stu-id="2bf26-109">**Microsoft.Quantum.Standard**</span></span>](https://www.nuget.org/packages/Microsoft.Quantum.Standard) | <span data-ttu-id="2bf26-110">Zahrnuto ve výchozím nastavení</span><span class="sxs-lookup"><span data-stu-id="2bf26-110">Included by default</span></span> |
| [<span data-ttu-id="2bf26-111">Kvantová chemická knihovna</span><span class="sxs-lookup"><span data-stu-id="2bf26-111">Quantum chemistry library</span></span>](xref:microsoft.quantum.chemistry.concepts.intro) | [<span data-ttu-id="2bf26-112">**Microsoft.Quantum.Chemistry**</span><span class="sxs-lookup"><span data-stu-id="2bf26-112">**Microsoft.Quantum.Chemistry**</span></span>](https://www.nuget.org/packages/Microsoft.Quantum.Chemistry) | |
| [<span data-ttu-id="2bf26-113">Kvantová numerická knihovna</span><span class="sxs-lookup"><span data-stu-id="2bf26-113">Quantum numerics library</span></span>](xref:microsoft.quantum.numerics.intro) | [<span data-ttu-id="2bf26-114">**Microsoft.... NUMERIC**</span><span class="sxs-lookup"><span data-stu-id="2bf26-114">**Microsoft.Quantum.Numerics**</span></span>](https://www.nuget.org/packages/Microsoft.Quantum.Numerics) | |
| [<span data-ttu-id="2bf26-115">Knihovna pro kvantové strojové učení</span><span class="sxs-lookup"><span data-stu-id="2bf26-115">Quantum machine learning library</span></span>](xref:microsoft.quantum.libraries.machine-learning.intro) | [<span data-ttu-id="2bf26-116">**Microsoft.Quantum.MachineLearning**</span><span class="sxs-lookup"><span data-stu-id="2bf26-116">**Microsoft.Quantum.MachineLearning**</span></span>](https://www.nuget.org/packages/Microsoft.Quantum.MachineLearning) | |

<span data-ttu-id="2bf26-117">Jakmile nainstalujete sadu pro vývoj s využitím provozu s preferovaným prostředím a jazykem hostitele, můžete snadno přidávat knihovny do samostatných projektů Q # bez nutnosti další instalace.</span><span class="sxs-lookup"><span data-stu-id="2bf26-117">Once you have installed the Quantum Development Kit for use with your preferred environment and host language, you can easily add libraries to individual Q# projects without any further installation.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf26-118">Některé knihovny Q # můžou fungovat dobře s dalšími nástroji, které fungují společně s programy Q # nebo které se integrují s vašimi hostitelskými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="2bf26-118">Some Q# libraries may work well with additional tools that work alongside your Q# programs, or that integrate with your host applications.</span></span>
> <span data-ttu-id="2bf26-119">Například [pokyny k instalaci knihovny chemického](xref:microsoft.quantum.chemistry.concepts.installation) zpracování popisují, jak použít balíček [ **Microsoft. NWChem. chemie** ](https://www.nuget.org/packages/Microsoft.Quantum.Chemistry) společně s platformou výpočetních dat a jak nainstalovat `qdk-chem` nástroje příkazového řádku pro práci s daty ze chemie.</span><span class="sxs-lookup"><span data-stu-id="2bf26-119">For example, the [chemistry library installation instructions](xref:microsoft.quantum.chemistry.concepts.installation) describe how to use the [**Microsoft.Quantum.Chemistry** package](https://www.nuget.org/packages/Microsoft.Quantum.Chemistry) together with the NWChem computational chemistry platform, and how to install the `qdk-chem` command-line tools for working with quantum chemistry data.</span></span>

## <a name="q-command-line-applications-or-net-interopability"></a>[<span data-ttu-id="2bf26-120">Aplikace příkazového řádku Q # nebo interoperabilita rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="2bf26-120">Q# command-line applications or .NET interopability</span></span>](#tab/tabid-csproj)

<span data-ttu-id="2bf26-121">**Příkazový řádek nebo Visual Studio Code:** Pomocí příkazového řádku samostatně nebo v rámci Visual Studio Code můžete pomocí `dotnet` příkazu přidat do projektu odkaz na balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="2bf26-121">**Command line or Visual Studio Code:** Using the command line on its own or from within Visual Studio Code, you can use the `dotnet` command to add a NuGet package reference to your project.</span></span>
<span data-ttu-id="2bf26-122">Pokud například chcete přidat balíček [**Microsoft. probíhat. Numerics**](https://www.nuget.org/packages/Microsoft.Quantum.Numerics) , spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="2bf26-122">For example, to add the [**Microsoft.Quantum.Numerics**](https://www.nuget.org/packages/Microsoft.Quantum.Numerics) package, run the following command:</span></span>

```dotnetcli
dotnet add package Microsoft.Quantum.Numerics
```

<span data-ttu-id="2bf26-123">**Visual Studio:** Pokud používáte sadu Visual Studio 2019 nebo novější, můžete přidat další balíčky Q # pomocí Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="2bf26-123">**Visual Studio:** If you are using Visual Studio 2019 or later, you can add additional Q# packages using the NuGet Package Manager.</span></span>
<span data-ttu-id="2bf26-124">Načtení balíčku:</span><span class="sxs-lookup"><span data-stu-id="2bf26-124">To load a package:</span></span> 
1. <span data-ttu-id="2bf26-125">Otevřete projekt v aplikaci Visual Studio a v nabídce **projekt** vyberte **Spravovat balíčky NuGet...**</span><span class="sxs-lookup"><span data-stu-id="2bf26-125">With a project open in Visual Studio, select **Manage NuGet Packages...** from the **Project** menu.</span></span>

2. <span data-ttu-id="2bf26-126">Klikněte na tlačítko **Procházet**, vyberte možnost **Zahrnout předprodejní** a vyhledejte název balíčku "Microsoft..... Numerics".</span><span class="sxs-lookup"><span data-stu-id="2bf26-126">Click **Browse**, select **Include prerelease** and search for the package name "Microsoft.Quantum.Numerics".</span></span> <span data-ttu-id="2bf26-127">Zobrazí se seznam balíčků, které jsou k dispozici ke stažení.</span><span class="sxs-lookup"><span data-stu-id="2bf26-127">This will list the packages available for download.</span></span>

3. <span data-ttu-id="2bf26-128">Najeďte myší na **Microsoft. propočty. čísel** a kliknutím na šipku dolů napravo od čísla verze nainstalujte balíček numerických verzí.</span><span class="sxs-lookup"><span data-stu-id="2bf26-128">Hover over **Microsoft.Quantum.Numerics** and click the downward-pointing arrow to the right of the version number to install the numerics package.</span></span>

<span data-ttu-id="2bf26-129">Další podrobnosti najdete v příručce k [uživatelskému rozhraní Správce balíčků](https://docs.microsoft.com/nuget/tools/package-manager-ui).</span><span class="sxs-lookup"><span data-stu-id="2bf26-129">For more details, see the [Package Manager UI guide](https://docs.microsoft.com/nuget/tools/package-manager-ui).</span></span>

<span data-ttu-id="2bf26-130">Alternativně můžete použít konzolu Správce balíčků k přidání knihovny numerické aplikace do projektu prostřednictvím rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="2bf26-130">Alternatively, you can use the Package Manager Console to add the numerics library to your project via the command line interface.</span></span>

![Použití konzoly Správce balíčků z příkazového řádku](~/media/vs2017-nuget-console-menu.png)

<span data-ttu-id="2bf26-132">V konzole správce balíčků spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="2bf26-132">From the Package Manager Console, run the following:</span></span>

```
Install-Package Microsoft.Quantum.Numerics
```

<span data-ttu-id="2bf26-133">Další podrobnosti najdete v [Průvodci konzolou správce balíčků](https://docs.microsoft.com/nuget/tools/package-manager-console).</span><span class="sxs-lookup"><span data-stu-id="2bf26-133">For more details, see the [Package Manager Console guide](https://docs.microsoft.com/nuget/tools/package-manager-console).</span></span>

## <a name="iq-notebooks"></a>[<span data-ttu-id="2bf26-134">SWEETIQ počet poznámkových bloků</span><span class="sxs-lookup"><span data-stu-id="2bf26-134">IQ# Notebooks</span></span>](#tab/tabid-notebook)

<span data-ttu-id="2bf26-135">Další balíčky můžete zpřístupnit pro použití v poznámkovém bloku SWEETIQ # pomocí [ `%package` příkazu Magic](xref:microsoft.quantum.iqsharp.magic-ref.package).</span><span class="sxs-lookup"><span data-stu-id="2bf26-135">You can make additional packages available for use in an IQ# Notebook by using the [`%package` magic command](xref:microsoft.quantum.iqsharp.magic-ref.package).</span></span>
<span data-ttu-id="2bf26-136">Pokud například chcete přidat balíček [**Microsoft. sweetiq. Numerics**](https://www.nuget.org/packages/Microsoft.Quantum.Numerics) pro použití v poznámkovém bloku #, spusťte následující příkaz v buňce s poznámkovým blokem:</span><span class="sxs-lookup"><span data-stu-id="2bf26-136">For example, to add the [**Microsoft.Quantum.Numerics**](https://www.nuget.org/packages/Microsoft.Quantum.Numerics) package for use in an IQ# Notebook, run the following command in a notebook cell:</span></span>

```
%package Microsoft.Quantum.Numerics
```

<span data-ttu-id="2bf26-137">Po tomto příkazu je balíček dostupný pro všechny buňky v poznámkovém bloku.</span><span class="sxs-lookup"><span data-stu-id="2bf26-137">Following this command, the package is available to any cells within the notebook.</span></span>
<span data-ttu-id="2bf26-138">Pokud chcete balíček zpřístupnit z kódu Q # v aktuálním pracovním prostoru, po přidání balíčku znovu načtěte tento pracovní prostor:</span><span class="sxs-lookup"><span data-stu-id="2bf26-138">To make the package available from Q# code in the current workspace, reload the workspace after adding your package:</span></span>

```
%workspace reload
```

## <a name="python-interoperability"></a>[<span data-ttu-id="2bf26-139">Interoperabilita Pythonu</span><span class="sxs-lookup"><span data-stu-id="2bf26-139">Python interoperability</span></span>](#tab/tabid-python)


<span data-ttu-id="2bf26-140">Další balíčky můžete zpřístupnit pro použití v hostitelském programu Pythonu pomocí [`qsharp.packages.add`](https://docs.microsoft.com/python/qsharp/qsharp.packages.packages) metody.</span><span class="sxs-lookup"><span data-stu-id="2bf26-140">You can make additional packages available for use in a Python host program by using the [`qsharp.packages.add`](https://docs.microsoft.com/python/qsharp/qsharp.packages.packages) method.</span></span>
<span data-ttu-id="2bf26-141">Pokud například chcete přidat balíček [**Microsoft. sweetiq. Numerics**](https://www.nuget.org/packages/Microsoft.Quantum.Numerics) pro použití v poznámkovém bloku #, spusťte následující kód Pythonu:</span><span class="sxs-lookup"><span data-stu-id="2bf26-141">For example, to add the [**Microsoft.Quantum.Numerics**](https://www.nuget.org/packages/Microsoft.Quantum.Numerics) package for use in an IQ# Notebook, run the following Python code:</span></span>

```python
import qsharp
qsharp.packages.add("Microsoft.Quantum.Numerics")
```

<span data-ttu-id="2bf26-142">Po provedení tohoto příkazu bude balíček dostupný pro všechny kompilované kódy Q # pomocí `qsharp.compile` .</span><span class="sxs-lookup"><span data-stu-id="2bf26-142">Following this command, the package will be made available to any Q# code compiled using `qsharp.compile`.</span></span>
<span data-ttu-id="2bf26-143">Pokud chcete balíček zpřístupnit z kódu Q # v aktuálním pracovním prostoru, po přidání balíčku znovu načtěte tento pracovní prostor:</span><span class="sxs-lookup"><span data-stu-id="2bf26-143">To make the package available from Q# code in the current workspace, reload the workspace after adding your package:</span></span>

```python
qsharp.reload()
```

***