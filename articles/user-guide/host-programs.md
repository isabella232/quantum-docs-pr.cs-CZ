---
title: 'Způsoby spuštění programu Q #'
description: 'Přehled různých způsobů spouštění programů Q #. Z příkazového řádku, poznámkových bloků Q # Jupyter a klasických hostitelských programů v Pythonu nebo v jazyce .NET.'
author: gillenhaalb
ms.author: a-gibec@microsoft.com
ms.date: 05/15/2020
ms.topic: article
uid: microsoft.quantum.guide.host-programs
ms.openlocfilehash: 132c138d7c392ed2b4bd3d0079180b68adae4cfc
ms.sourcegitcommit: a3775921db1dc5c653c97b8fa8fe2c0ddd5261ff
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887656"
---
# <a name="ways-to-run-a-q-program"></a><span data-ttu-id="3fe5b-104">Způsoby spuštění programu Q #</span><span class="sxs-lookup"><span data-stu-id="3fe5b-104">Ways to run a Q# program</span></span>

<span data-ttu-id="3fe5b-105">Jednou z největších silou pro vývojová prostředí pro životní prostředí je jeho flexibilita napříč platformami a vývojovým prostředím.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-105">One of the Quantum Development Kit's greatest strengths is its flexibility across platforms and development environments.</span></span>
<span data-ttu-id="3fe5b-106">To ale také znamená, že noví uživatelé Q # můžou najít zaměňování nebo zahlcení řadou možností, které najdete v [instalační příručce](xref:microsoft.quantum.install).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-106">However, this also means that new Q# users may find themselves confused or overwhelmed by the numerous options found in the [install guide](xref:microsoft.quantum.install).</span></span>
<span data-ttu-id="3fe5b-107">Na této stránce vysvětlete, co se stane, když se spustí program Q #, a porovnejte různé způsoby, jak to uživatelé můžou udělat.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-107">On this page, we explain what happens when a Q# program is run, and compare the different ways in which users can do so.</span></span>

<span data-ttu-id="3fe5b-108">Zásadním rozdílem je, že Q # lze spustit:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-108">A primary distinction is that Q# can be run:</span></span>
- <span data-ttu-id="3fe5b-109">jako samostatná aplikace, kde Q # je jediný jazyk, který je součástí programu a který je vyvolán přímo.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-109">as a standalone application, where Q# is the only language involved and the program is invoked directly.</span></span> <span data-ttu-id="3fe5b-110">Do této kategorie ve skutečnosti patří dvě metody:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-110">Two methods actually fall in this category:</span></span>
  - <span data-ttu-id="3fe5b-111">rozhraní příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="3fe5b-111">the command line interface</span></span>
  - <span data-ttu-id="3fe5b-112">Aplikace Jupyter Notebook v Q#</span><span class="sxs-lookup"><span data-stu-id="3fe5b-112">Q# Jupyter Notebooks</span></span>
- <span data-ttu-id="3fe5b-113">s dalším *hostitelským programem*, který je napsán v Pythonu nebo v jazyce .NET (např. C# nebo F #), který potom vyvolá program a může pokračovat ve zpracování vrácených výsledků.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-113">with an additional *host program*, written in Python or a .NET language (e.g. C# or F#), which then invokes the program and can further process returned results.</span></span>

<span data-ttu-id="3fe5b-114">Abychom těmto procesům a jejich rozdílům nejlépe pochopili, Uvažujme o jednoduchém programu Q # a porovnejte způsob, jakým je možné ho spustit.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-114">To best understand these processes and their differences, we consider a simple Q# program and compare the ways it can be executed.</span></span>

## <a name="basic-q-program"></a><span data-ttu-id="3fe5b-115">Základní program Q #</span><span class="sxs-lookup"><span data-stu-id="3fe5b-115">Basic Q# program</span></span>

<span data-ttu-id="3fe5b-116">Základní program pro vystavování se může skládat z přípravy qubit do stejné pozice stavů $ \ket {0} $ a $ \ket {1} $, měření a vrácení výsledku, který bude náhodně buď jedna z těchto dvou stavů, se stejnou pravděpodobností.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-116">A basic quantum program might consist of preparing a qubit in an equal superposition of states $\ket{0}$ and $\ket{1}$, measuring it, and returning the result, which will be randomly either one of these two states with equal probability.</span></span>
<span data-ttu-id="3fe5b-117">Tento proces je skutečně v jádru pro rychlý Start [generátoru náhodných čísel](xref:microsoft.quantum.quickstarts.qrng) .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-117">Indeed, this process is at the core of the [quantum random number generator](xref:microsoft.quantum.quickstarts.qrng) quickstart.</span></span>

<span data-ttu-id="3fe5b-118">V Q # by to bylo provedeno následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-118">In Q#, this would be performed by the following code:</span></span>

```qsharp
        using (q = Qubit()) {    // allocates qubit for use (automatically in |0>)
            H(q);                // puts qubit in superposition of |0> and |1>
            return MResetZ(q);   // measures qubit, returns result (and resets it to |0> before deallocation)
        }
```

<span data-ttu-id="3fe5b-119">Samotný kód však nelze spustit pomocí Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-119">However, this code alone can't be executed by Q#.</span></span>
<span data-ttu-id="3fe5b-120">V takovém případě musí sestavovat tělo [operace](xref:microsoft.quantum.guide.basics#q-operations-and-functions), která se pak spustí při volání---, a to buď přímo, nebo jinou operací.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-120">For that, it needs to make up the body of an [operation](xref:microsoft.quantum.guide.basics#q-operations-and-functions), which is then executed when called---either directly or by another operation.</span></span> <span data-ttu-id="3fe5b-121">Proto můžete napsat operaci následujícího formuláře:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-121">Hence, you can write an operation of the following form:</span></span>
```qsharp
    operation MeasureSuperposition() : Result {
        using (q = Qubit()) {
            H(q);
            return MResetZ(q);
        }
    }
```
<span data-ttu-id="3fe5b-122">Definovali jste operaci, `MeasureSuperposition` která nepřijímá žádné vstupy a vrací hodnotu typu [Result](xref:microsoft.quantum.guide.types).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-122">You have defined an operation, `MeasureSuperposition`, which takes no inputs and returns a value of type [Result](xref:microsoft.quantum.guide.types).</span></span>

<span data-ttu-id="3fe5b-123">I když příklady na této stránce sestávají jenom s *operacemi*q #, všechny koncepty, které budeme projednávat, se budou týkat i *funkcí*q #, a proto je budeme v souhrnně *označovat jako možné*.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-123">While the examples on this page only consist of Q# *operations*, all of the concepts we will discuss pertain equally to Q# *functions*, and therefore we refer to them collectively as *callables*.</span></span> <span data-ttu-id="3fe5b-124">Jejich rozdíly jsou popsány v tématu [základní informace o funkci Q #: operace a funkce](xref:microsoft.quantum.guide.basics#q-operations-and-functions)a další informace o jejich definování najdete v tématu [operace a funkce](xref:microsoft.quantum.guide.operationsfunctions).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-124">Their differences are discussed at [Q# basics: operations and functions](xref:microsoft.quantum.guide.basics#q-operations-and-functions), and more details on defining them can be found at [Operations and functions](xref:microsoft.quantum.guide.operationsfunctions).</span></span>

### <a name="callable-defined-in-a-q-file"></a><span data-ttu-id="3fe5b-125">Navolatelné v souboru Q #</span><span class="sxs-lookup"><span data-stu-id="3fe5b-125">Callable defined in a Q# file</span></span>

<span data-ttu-id="3fe5b-126">Volání je přesně to, co se volá a spouští se Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-126">The callable is precisely what's called and run by Q#.</span></span>
<span data-ttu-id="3fe5b-127">Nicméně vyžaduje několik dalších přídavků, které obsahují úplný `*.qs` soubor Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-127">However, it requires a few more additions to comprise a full `*.qs` Q# file.</span></span>

<span data-ttu-id="3fe5b-128">Všechny typy Q # a volatelné (ty, které definujete i u těchto vnitřních jazyků) jsou definovány v rámci *oborů názvů*, které poskytují každý úplný název, na který lze následně odkazovat.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-128">All Q# types and callables (both those you define and those intrinsic to the language) are defined within *namespaces*, which provide each a full name that can then be referenced.</span></span>

<span data-ttu-id="3fe5b-129">Například [`H`](xref:microsoft.quantum.intrinsic.h) [`MResetZ`](xref:microsoft.quantum.measurement.mresetz) operace a se nacházejí v [`Microsoft.Quantum.Instrinsic`](xref:microsoft.quantum.intrinsic) [`Microsoft.Quantum.Measurement`](xref:microsoft.quantum.measurement) oborech názvů a (součást [standardních knihoven Q #](xref:microsoft.quantum.qsharplibintro)).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-129">For example, the [`H`](xref:microsoft.quantum.intrinsic.h) and [`MResetZ`](xref:microsoft.quantum.measurement.mresetz) operations are found in the [`Microsoft.Quantum.Instrinsic`](xref:microsoft.quantum.intrinsic) and [`Microsoft.Quantum.Measurement`](xref:microsoft.quantum.measurement) namespaces (part of the [Q# Standard Libraries](xref:microsoft.quantum.qsharplibintro)).</span></span>
<span data-ttu-id="3fe5b-130">V takovém případě mohou být vždy volány prostřednictvím jejich *úplných* názvů, `Microsoft.Quantum.Intrinsic.H(<qubit>)` `Microsoft.Quantum.Measurement.MResetZ(<qubit>)` ale vždy to vede k tomu, že by to vedlo k velmi zbytečnému kódu.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-130">As such, they can always be called via their *full* names, `Microsoft.Quantum.Intrinsic.H(<qubit>)` and `Microsoft.Quantum.Measurement.MResetZ(<qubit>)`, but always doing this would lead to very cluttered code.</span></span>

<span data-ttu-id="3fe5b-131">Místo toho `open` příkazy umožňují volat odkazování pomocí výstižnější zkratky, jak jsme udělali v těle operace výše.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-131">Instead, `open` statements allow callables to be referenced with more concise shorthand, as we've done in the operation body above.</span></span>
<span data-ttu-id="3fe5b-132">Úplný soubor Q # obsahující naši operaci se proto skládá z definování vlastního oboru názvů, otevření oborů názvů pro ty, které používají naši operaci, a pak naší operace:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-132">The full Q# file containing our operation would therefore consist of defining our own namespace, opening the namespaces for those callables our operation uses, and then our operation:</span></span>

```qsharp
namespace NamespaceName {
    open Microsoft.Quantum.Intrinsic;     // for the H operation
    open Microsoft.Quantum.Measurement;   // for MResetZ

    operation MeasureSuperposition() : Result {
        using (q = Qubit()) { 
            H(q);
            return MResetZ(q);
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="3fe5b-133">Obory názvů lze také *aliasovat* při otevření, což může být užitečné v případě konfliktu názvů volat/typu ve dvou oborech názvů.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-133">Namespaces can also be *aliased* when opened, which can be helpful if callable/type names in two namespaces conflict.</span></span>
> <span data-ttu-id="3fe5b-134">Například můžeme použít `open Microsoft.Quantum.Instrinsic as NamespaceWithH;` výše a potom zavolat `H` prostřednictvím `NamespaceWithH.H(<qubit>)` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-134">For example, we could instead use `open Microsoft.Quantum.Instrinsic as NamespaceWithH;` above, and then call `H` via `NamespaceWithH.H(<qubit>)`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fe5b-135">Jedna výjimka pro všechny Toto je [`Microsoft.Quantum.Core`](xref:microsoft.quantum.core) obor názvů, který je vždy automaticky otevřen.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-135">One exception to all of this is the [`Microsoft.Quantum.Core`](xref:microsoft.quantum.core) namespace, which is always automatically opened.</span></span>
> <span data-ttu-id="3fe5b-136">Proto lze volat jako [`Length`](xref:microsoft.quantum.core.length) vždy použít přímo.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-136">Therefore, callables like [`Length`](xref:microsoft.quantum.core.length) can always be used directly.</span></span>

### <a name="execution-on-target-machines"></a><span data-ttu-id="3fe5b-137">Spouštění na cílových počítačích</span><span class="sxs-lookup"><span data-stu-id="3fe5b-137">Execution on target machines</span></span>

<span data-ttu-id="3fe5b-138">Nyní bude obecný model spuštění programu Q # jasný.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-138">Now the general execution model of a Q# program becomes clear.</span></span>

<br/>
<img src="../media/hostprograms_general_execution_model.png" alt="Q# program execution diagram" width="400">

<span data-ttu-id="3fe5b-139">Za prvé, konkrétní spuštění, které se má spustit, má přístup k jakýmkoli jiným přívolat a typům definovaným ve stejném oboru názvů.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-139">Firstly, the specific callable to be executed has access to any other callables and types defined in the same namespace.</span></span>
<span data-ttu-id="3fe5b-140">Také k nim přistupuje z libovolné [knihovny Q #](xref:microsoft.quantum.libraries), ale musí být odkazovány buď prostřednictvím jejich úplného názvu, nebo pomocí `open` příkazů popsaných výše.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-140">It also access those from any of the [Q# libraries](xref:microsoft.quantum.libraries), but those must be referenced either via their full name, or through the use of `open` statements described above.</span></span>

<span data-ttu-id="3fe5b-141">Sama se pak spustí na *[cílovém počítači](xref:microsoft.quantum.machines)*.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-141">The callable itself is then executed on a *[target machine](xref:microsoft.quantum.machines)*.</span></span>
<span data-ttu-id="3fe5b-142">Tyto cílové počítače můžou být skutečným hardwarem nebo s více simulátory, které jsou k dispozici jako součást QDK.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-142">Such target machines can be actual quantum hardware or the multiple simulators available as part of the QDK.</span></span>
<span data-ttu-id="3fe5b-143">Pro naše účely je nejužitečnější cílový počítač instancí [simulátoru s plným stavem](xref:microsoft.quantum.machines.full-state-simulator), `QuantumSimulator` který počítá chování programu, jako kdyby bylo spuštěno na počítači se systémem, který je bezproblémový.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-143">For our purposes here, the most useful target machine is an instance of the [full-state simulator](xref:microsoft.quantum.machines.full-state-simulator), `QuantumSimulator`, which calculates the program's behavior as if it were being executed on a noise-free quantum computer.</span></span>

<span data-ttu-id="3fe5b-144">Zatím jsme popsali, co se stane, když se spustí konkrétní Q # volat.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-144">So far, we've described what happens when a specific Q# callable is being executed.</span></span>
<span data-ttu-id="3fe5b-145">Bez ohledu na to, zda je v samostatné aplikaci nebo v hostitelském programu používáno Q #, je tento obecný proces více nebo méně stejný,---QDK, tedy flexibilitu.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-145">Regardless of whether Q# is used in a standalone application or with a host program, this general process is more or less the same---hence the QDK's flexibility.</span></span>
<span data-ttu-id="3fe5b-146">Rozdíly mezi různými způsoby volání do vývojového prostředí pro plnění obsahu si proto samy odhalí, *jak* je volání Q # Called provedeno a v jakém způsobem jsou vráceny výsledky.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-146">The differences between the different ways of calling into the Quantum Development Kit therefore reveal themselves in *how* that Q# callable is called to be executed, and in what manner any results are returned.</span></span>
<span data-ttu-id="3fe5b-147">Přesněji řečeno, rozdíly obtéká kolem</span><span class="sxs-lookup"><span data-stu-id="3fe5b-147">More specifically, the differences revolve around</span></span> 
1. <span data-ttu-id="3fe5b-148">označuje, kterou hodnotu Q # volat se má provést.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-148">indicating which Q# callable is to be executed,</span></span>
2. <span data-ttu-id="3fe5b-149">jak jsou k dispozici možné argumenty pro možnost použití,</span><span class="sxs-lookup"><span data-stu-id="3fe5b-149">how potential callable arguments are provided,</span></span>
3. <span data-ttu-id="3fe5b-150">zadání cílového počítače, na kterém se má spustit, a</span><span class="sxs-lookup"><span data-stu-id="3fe5b-150">specifying the target machine on which to execute it, and</span></span>
4. <span data-ttu-id="3fe5b-151">způsob, jakým jsou vráceny výsledky.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-151">how any results are returned.</span></span>

<span data-ttu-id="3fe5b-152">Nejdřív se podíváme na to, jak se to dělá pomocí samostatné aplikace Q # z příkazového řádku, a pak pokračujte pomocí hostitelských programů Pythonu a C#.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-152">First, we discuss how this is done with the Q# standalone application from the command line, and then proceed to using Python and C# host programs.</span></span>
<span data-ttu-id="3fe5b-153">Vyhrazujeme si samostatnou aplikaci poznámkových bloků Q # Jupyter, protože na rozdíl od prvních tří nezáleží na tom, že se jedná o místní funkce na střed souboru Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-153">We reserve the standalone application of Q# Jupyter Notebooks for last, because unlike the first three, it's primary functionality does not center around a local Q# file.</span></span>

> [!NOTE]
> <span data-ttu-id="3fe5b-154">I když ho v těchto příkladech neilustruje, jedná se o jeden společný vztah mezi metodami spuštění, protože všechny zprávy vytištěné z programu Q # (například v případě [`Message`](xref:microsoft.quantum.intrinsic.message) [`DumpMachine`](xref:microsoft.quantum.diagnostics.dumpmachine) , že) se obvykle vždy vytisknou do příslušné konzoly.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-154">Although we don't illustrate it in these examples, one commonality between the execution methods is that any messages printed from inside the Q# program (by way of [`Message`](xref:microsoft.quantum.intrinsic.message) or [`DumpMachine`](xref:microsoft.quantum.diagnostics.dumpmachine), for example) will typically always be printed to the respective console.</span></span>

## <a name="q-from-the-command-line"></a><span data-ttu-id="3fe5b-155">Q # z příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="3fe5b-155">Q# from the command line</span></span>
<span data-ttu-id="3fe5b-156">Jedním z nejjednodušších způsobů, jak začít psát do programu Q #, je zabránit tomu, abyste se mohli zcela starat o samostatné soubory a druhý jazyk.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-156">One of the easiest ways to get started writing Q# programs is to avoid worrying about separate files and a second language altogether.</span></span>
<span data-ttu-id="3fe5b-157">Pomocí Visual Studio Code nebo sady Visual Studio s rozšířením QDK umožňuje bezproblémové pracovní postup, při kterém se spustí Q #, který se dá volat jenom z jednoho souboru Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-157">Using Visual Studio Code or Visual Studio with the QDK extension allows for a seamless work flow in which we run Q# callables from only a single Q# file.</span></span>

<span data-ttu-id="3fe5b-158">V tomto případě budeme vyvolávat spuštění programu tím, že zadáte</span><span class="sxs-lookup"><span data-stu-id="3fe5b-158">For this, we will ultimately invoke the program's execution by entering</span></span>
```dotnetcli
dotnet run
```
<span data-ttu-id="3fe5b-159">na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-159">in the command line.</span></span>
<span data-ttu-id="3fe5b-160">Nejjednodušší pracovní postup je v případě, že je umístění adresáře terminálu stejné jako soubor Q #, který je možné snadno zpracovat vedle úprav souborů Q # pomocí integrovaného terminálu v VS Code.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-160">The simplest workflow is when the terminal's directory location is the same as the Q# file, which can be easily handled alongside Q# file editing by using the integrated terminal in VS Code, for example.</span></span>
<span data-ttu-id="3fe5b-161">[ `dotnet run` Příkaz](https://docs.microsoft.com/dotnet/core/tools/dotnet-run) však akceptuje mnoho možností a program lze také spustit z jiného umístění pouhým poskytnutím `--project <PATH>` umístění souboru Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-161">However, the [`dotnet run` command](https://docs.microsoft.com/dotnet/core/tools/dotnet-run) accepts numerous options, and the program can also be run from a different location by simply providing `--project <PATH>` with the location of the Q# file.</span></span>


### <a name="add-entry-point-to-q-file"></a><span data-ttu-id="3fe5b-162">Přidat vstupní bod do souboru Q #</span><span class="sxs-lookup"><span data-stu-id="3fe5b-162">Add entry point to Q# file</span></span>

<span data-ttu-id="3fe5b-163">Většina souborů Q # bude obsahovat více než jednu vykonatelné, takže je potřeba, aby kompilátor věděl, *který* volat, aby se spustil při zadání `dotnet run` příkazu.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-163">Most Q# files will contain more than one callable, so naturally we need to let the compiler know *which* callable to execute when we provide the `dotnet run` command.</span></span>
<span data-ttu-id="3fe5b-164">To se provádí jednoduchou změnou samotného souboru Q #:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-164">This is done with a simple change to the Q# file itself:</span></span> 
    - <span data-ttu-id="3fe5b-165">Přidejte řádek, který `@EntryPoint()` je přímo před volat.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-165">add a line with `@EntryPoint()` directly preceding the callable.</span></span>

<span data-ttu-id="3fe5b-166">Náš soubor výše by se proto stal</span><span class="sxs-lookup"><span data-stu-id="3fe5b-166">Our file from above would therefore become</span></span>
```qsharp
namespace NamespaceName {
    open Microsoft.Quantum.Intrinsic;     // for the H operation
    open Microsoft.Quantum.Measurement;   // for MResetZ

    @EntryPoint()
    operation MeasureSuperposition() : Result {
        using (q = Qubit()) { 
            H(q);
            return MResetZ(q);
        }
    }
}
```

<span data-ttu-id="3fe5b-167">Nyní volání `dotnet run` z příkazového řádku vede ke `MeasureSuperposition` spuštění a vrácená hodnota je poté vytištěna přímo na terminálu.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-167">Now, a call of `dotnet run` from the command line leads to `MeasureSuperposition` being run, and the returned value is then printed directly to the terminal.</span></span>
<span data-ttu-id="3fe5b-168">Zobrazí se buď `One` nebo `Zero` vytištěno.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-168">So, you will see either `One` or `Zero` printed.</span></span> 

<span data-ttu-id="3fe5b-169">Mějte na paměti, že pokud máte více než jedno navýšení volat, `MeasureSuperposition` bude spuštěno.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-169">Note that it doesn't matter if you have more callables defined below it, only `MeasureSuperposition` will be run.</span></span>
<span data-ttu-id="3fe5b-170">Kromě toho není k dispozici žádný problém, pokud vaše volat obsahuje [dokumentační komentáře](xref:microsoft.quantum.guide.filestructure#documentation-comments) před jeho deklarací, `@EntryPoint()` atribut lze jednoduše umístit nad něj.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-170">Additionally, it's no problem if your callable includes [documentation comments](xref:microsoft.quantum.guide.filestructure#documentation-comments) before its declaration, the `@EntryPoint()` attribute can be simply placed above them.</span></span>

### <a name="callable-arguments"></a><span data-ttu-id="3fe5b-171">Volat argumenty</span><span class="sxs-lookup"><span data-stu-id="3fe5b-171">Callable arguments</span></span>

<span data-ttu-id="3fe5b-172">Zatím jsme se považovali jenom na operace, které přebírají žádné vstupy.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-172">So far, we've only considered an operation that takes no inputs.</span></span>
<span data-ttu-id="3fe5b-173">Předpokládejme, že jsme chtěli provést podobnou operaci, ale na více qubits---počet, který je k dispozici jako argument.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-173">Suppose we wanted to perform a similar operation, but on multiple qubits---the number of which is provided as an argument.</span></span>
<span data-ttu-id="3fe5b-174">Taková operace by mohla být zapsána jako</span><span class="sxs-lookup"><span data-stu-id="3fe5b-174">Such an operation could be written as</span></span>
```qsharp
    operation MeasureSuperpositionArray(n : Int) : Result[] {
        using (qubits = Qubit[n]) {              // allocate a register of n qubits
            ApplyToEach(H, qubits);              // apply H to each qubit in the register
            return ForEach(MResetZ, qubits);     // perform MResetZ on each qubit, returns the resulting array
        }
    }
```
<span data-ttu-id="3fe5b-175">kde vrácená hodnota je pole výsledků měření.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-175">where the returned value is an array of the measurement results.</span></span>
<span data-ttu-id="3fe5b-176">Všimněte si, že [`ApplyToEach`](xref:microsoft.quantum.canon.applytoeach) a [`ForEach`](xref:microsoft.quantum.arrays.foreach) jsou [`Microsoft.Quantum.Canon`](xref:microsoft.quantum.canon) v [`Microsoft.Quantum.Arrays`](xref:microsoft.quantum.arrays) oborech názvů a, vyžadování dalších `open` příkazů pro každý z nich.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-176">Note that [`ApplyToEach`](xref:microsoft.quantum.canon.applytoeach) and [`ForEach`](xref:microsoft.quantum.arrays.foreach) are in the [`Microsoft.Quantum.Canon`](xref:microsoft.quantum.canon) and [`Microsoft.Quantum.Arrays`](xref:microsoft.quantum.arrays) namespaces, requiring additional `open` statements for each.</span></span>

<span data-ttu-id="3fe5b-177">Pokud přesouváme `@EntryPoint()` atribut tak, aby předcházel této nové operaci (Všimněte si, že v souboru může být jenom jeden řádek), pokus o jeho spuštění s jednoduchým `dotnet run` výsledkem je chybová zpráva, která indikuje, co je potřeba pro další možnosti příkazového řádku, a jak je vyjádřit.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-177">If we move the `@EntryPoint()` attribute to precede this new operation (note there can only be one such line in a file), attempting to run it with simply `dotnet run` results in an error message which indicates what additional command line options are required, and how to express them.</span></span>

<span data-ttu-id="3fe5b-178">Obecný formát příkazového řádku je ve skutečnosti `dotnet run [options]` a k dispozici jsou argumenty, které jsou zde k dispozici.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-178">The general format for the command line is actually `dotnet run [options]`, and callable arguments are provided there.</span></span>
<span data-ttu-id="3fe5b-179">V tomto případě `n` chybí argument a ukazuje, že je nutné zadat možnost `-n <n>` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-179">In this case, the argument `n` is missing, and it shows that we need to provide the option `-n <n>`.</span></span> <span data-ttu-id="3fe5b-180">Pro spuštění `MeasureSuperpositionArray` pro `n=4` qubits proto používáme</span><span class="sxs-lookup"><span data-stu-id="3fe5b-180">To run `MeasureSuperpositionArray` for `n=4` qubits, we therefore use</span></span>

```dotnetcli
dotnet run -n 4
```

<span data-ttu-id="3fe5b-181">získávání výstupu podobného</span><span class="sxs-lookup"><span data-stu-id="3fe5b-181">yielding an output similar to</span></span>

```output
[Zero,One,One,One]
```

<span data-ttu-id="3fe5b-182">Tento kurz rozšiřuje na více argumentů.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-182">This of course extends to multiple arguments.</span></span>

> [!NOTE]
> <span data-ttu-id="3fe5b-183">Názvy argumentů definované v `camelCase` jsou mírně změněny kompilátorem, aby byly přijaty jako vstupy Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-183">Argument names defined in `camelCase` are slightly altered by the compiler to be accepted as Q# inputs.</span></span> <span data-ttu-id="3fe5b-184">Například, pokud místo `n` , jsme použili název `numQubits` uvedený výše, a tento vstup by se zadal na příkazovém řádku pomocí `--num-qubits 4` místo `-n 4` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-184">For example, if instead of `n`, we used the name `numQubits` above, then this input would be provided in the command line via `--num-qubits 4` instead of `-n 4`.</span></span>

<span data-ttu-id="3fe5b-185">Chybová zpráva taky obsahuje další možnosti, které se dají použít, včetně toho, jak změnit cílový počítač.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-185">The error message also provides other options which can be used, including how to change the target machine.</span></span>

### <a name="different-target-machines"></a><span data-ttu-id="3fe5b-186">Různé cílové počítače</span><span class="sxs-lookup"><span data-stu-id="3fe5b-186">Different target machines</span></span>

<span data-ttu-id="3fe5b-187">Vzhledem k tomu, že výstupy z našich operací byly doposud očekávané výsledky jejich akce v reálném qubits, je jasné, že výchozí cílový počítač z příkazového řádku je quauntum simulátor `QuantumSimulator` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-187">As the outputs from our operations thus far have been the expected results of their action on real qubits, it's clear that the default target machine from the command line is the full-state quauntum simulator, `QuantumSimulator`.</span></span>
<span data-ttu-id="3fe5b-188">Dá se ale dát pokyn ke spuštění na konkrétním cílovém počítači s možností `--simulator` (nebo zkráceným `-s` ).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-188">However, we can instruct callables to be run on a specific target machine with the option `--simulator` (or the shorthand `-s`).</span></span>

<span data-ttu-id="3fe5b-189">Můžete ho například spustit na [`ResourcesEstimator`](xref:microsoft.quantum.machines.resources-estimator) :</span><span class="sxs-lookup"><span data-stu-id="3fe5b-189">For example, we could run it on [`ResourcesEstimator`](xref:microsoft.quantum.machines.resources-estimator):</span></span>

```dotnetcli
dotnet run -n 4 -s ResourcesEstimator
```

<span data-ttu-id="3fe5b-190">Vytištěný výstup je pak</span><span class="sxs-lookup"><span data-stu-id="3fe5b-190">The printed output is then</span></span>

```output
Metric          Sum
CNOT            0
QubitClifford   4
R               0
Measure         4
T               0
Depth           0
Width           4
BorrowedWidth   0
```

<span data-ttu-id="3fe5b-191">Podrobnosti o tom, co tyto metriky naznačují, najdete v tématu věnovaném [Estimator prostředků: metriky se nahlásily](xref:microsoft.quantum.machines.resources-estimator#metrics-reported).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-191">For details on what these metrics indicate, see [Resource estimator: metrics reported](xref:microsoft.quantum.machines.resources-estimator#metrics-reported).</span></span>

### <a name="command-line-execution-summary"></a><span data-ttu-id="3fe5b-192">Souhrn spuštění příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="3fe5b-192">Command line execution summary</span></span>
<br/>
<img src="../media/hostprograms_command_line_diagram.png" alt="Q# program from command line" width="700">

### <a name="non-q-dotnet-run-options"></a><span data-ttu-id="3fe5b-193">Možnosti bez Q # `dotnet run`</span><span class="sxs-lookup"><span data-stu-id="3fe5b-193">Non-Q# `dotnet run` options</span></span>

<span data-ttu-id="3fe5b-194">Jak jsme se na tuto možnost krátce zmínili `--project` , [ `dotnet run` příkaz](https://docs.microsoft.com/dotnet/core/tools/dotnet-run) také přijímá možnosti, které nesouvisí s argumenty volat v parametru Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-194">As we briefly mentioned above with the `--project` option, the [`dotnet run` command](https://docs.microsoft.com/dotnet/core/tools/dotnet-run) also accepts options unrelated to the Q# callable arguments.</span></span>
<span data-ttu-id="3fe5b-195">Pokud zadáváte oba druhy možností, `dotnet` musí být nejprve zadány možnosti specifické pro konkrétní parametry, následované oddělovač `--` a pak parametry specifické pro Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-195">If providing both kinds of options, the `dotnet`-specific options must be provided first, followed by a delimeter `--`, and then the Q#-specific options.</span></span>
<span data-ttu-id="3fe5b-196">Například specifiying cestu spolu s číslem qubits pro operaci výše, kterou by bylo provedeno prostřednictvím `dotnet run --project <PATH> -- -n <n>` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-196">For example, specifiying a path along with a number qubits for the operation above would be executed via `dotnet run --project <PATH> -- -n <n>`.</span></span>

## <a name="q-with-host-programs"></a><span data-ttu-id="3fe5b-197">Q # s hostitelskými programy</span><span class="sxs-lookup"><span data-stu-id="3fe5b-197">Q# with host programs</span></span>

<span data-ttu-id="3fe5b-198">S naším souborem Q # je alternativou pro volání operace nebo funkce přímo z příkazového řádku použití *hostitelského programu* v jiném klasickém jazyce.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-198">With our Q# file in hand, an alternative to calling an operation or function directly from the command line is to use a *host program* in another classical language.</span></span> <span data-ttu-id="3fe5b-199">Konkrétně to lze provést buď pomocí Pythonu, nebo jazyka .NET, jako je C# nebo F # (za účelem zkrácení budeme podrobnosti pouze C#).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-199">Specifically, this can be done with either Python or a .NET language such as C# or F# (for the sake of brevity we will only detail C# here).</span></span>
<span data-ttu-id="3fe5b-200">K povolení interoperability je potřeba trochu dalších nastavení, ale tyto podrobnosti najdete v [pokynech k instalaci](xref:microsoft.quantum.install).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-200">A little more setup is required to enable the interoperability, but those details can be found in the [install guides](xref:microsoft.quantum.install).</span></span>

<span data-ttu-id="3fe5b-201">V kostce nyní tato situace zahrnuje soubor hostitelského programu (například `*.py` nebo `*.cs` ) ve stejném umístění jako náš soubor Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-201">In a nutshell, the situation now includes a host program file (e.g. `*.py` or `*.cs`) in the same location as our Q# file.</span></span>
<span data-ttu-id="3fe5b-202">Nyní je *hostitelský* program, který se spustí, a v průběhu jeho provádění může volat konkrétní operace Q # a funkce ze souboru q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-202">It's now the *host* program that gets run, and in the course of its execution it can call specific Q# operations and functions from the Q# file.</span></span>
<span data-ttu-id="3fe5b-203">Základ interoperability je založen na kompilátoru Q # vytvoření obsahu souboru Q # přístupného pro hostitelský program, aby bylo možné je volat.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-203">The core of the interoperability is based on the Q# compiler making the contents of the Q# file accessible to the host program so that they can be called.</span></span>

<span data-ttu-id="3fe5b-204">Jednou z hlavních výhod používání hostitelského programu je to, že klasická data vrácená programem Q # je pak možné dále zpracovat v jazyce hostitele.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-204">One of the main benefits of using a host program is that the classical data returned by the Q# program can then be further processed in the host language.</span></span>
<span data-ttu-id="3fe5b-205">Může se jednat o některé pokročilé zpracování dat (například něco, co se v Q # nedaří provést interně) a potom na základě těchto výsledků zavolat další akce Q # nebo něco jednoduchého jako vykreslení výsledků Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-205">This could consist of some advanced data processing (e.g. something that can't be performed internally in Q#), and then calling further Q# actions based on those results, or something as simple as plotting the Q# results.</span></span>

<span data-ttu-id="3fe5b-206">Tady se zobrazí obecné schéma a v následující části se podíváme na konkrétní implementace pro Python a C#.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-206">The general scheme is shown here, and we discuss the specific implementations for Python and C# below.</span></span> <span data-ttu-id="3fe5b-207">Ukázku použití hostitelského programu F # najdete v [ukázkách interoperability .NET](https://github.com/microsoft/Quantum/tree/master/samples/interoperability/dotnet).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-207">A sample using an F# host program can be found at the [.NET interoperability samples](https://github.com/microsoft/Quantum/tree/master/samples/interoperability/dotnet).</span></span>

<br/>
<img src="../media/hostprograms_host_program_diagram.png" alt="Q# program from a host program" width="700">

> [!NOTE]
> <span data-ttu-id="3fe5b-208">`@EntryPoint()`Atribut použitý pro aplikace příkazového řádku Q # nelze použít s hostitelskými programy.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-208">The `@EntryPoint()` attribute used for Q# command line applications cannot be used with host programs.</span></span>
> <span data-ttu-id="3fe5b-209">Pokud se objeví v souboru Q #, který volá hostitel, bude vyvolána chyba.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-209">An error will be raised if it is present in the Q# file being called by a host.</span></span> 

<span data-ttu-id="3fe5b-210">Pro práci s různými hostitelskými programy nejsou v souboru Q # vyžadovány žádné změny `*.qs` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-210">To work with different host programs, there are no changes required to a `*.qs` Q# file.</span></span>
<span data-ttu-id="3fe5b-211">Následující hostitelské programy implementují všechny práce se stejným souborem Q #:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-211">The following host program implementations all work with the same Q# file:</span></span>

```qsharp
namespace NamespaceName {
    open Microsoft.Quantum.Intrinsic;     // contains H
    open Microsoft.Quantum.Measurement;   // MResetZ
    open Microsoft.Quantum.Canon;         // ApplyToEach
    open Microsoft.Quantum.Arrays;        // ForEach

    operation MeasureSuperposition() : Result {
        using (q = Qubit()) { 
            H(q);
            return MResetZ(q);
        }
    }

    operation MeasureSuperpositionArray(n : Int) : Result[] {
        using (qubits = Qubit[n]) {  
            ApplyToEach(H, qubits); 
            return ForEach(MResetZ, qubits);    
        }
    }
}
```

<span data-ttu-id="3fe5b-212">Vyberte kartu odpovídající vašemu hostitelskému jazyku, který vás zajímá.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-212">Select the tab corresponding to your host language of interest.</span></span>

### <a name="python"></a>[<span data-ttu-id="3fe5b-213">Python</span><span class="sxs-lookup"><span data-stu-id="3fe5b-213">Python</span></span>](#tab/tabid-python)
<span data-ttu-id="3fe5b-214">Hostitelský program Pythonu je vytvořený takto:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-214">A Python host program is constructed as follows:</span></span>
1. <span data-ttu-id="3fe5b-215">Importujte `qsharp` modul, který registruje zavaděč modulů pro interoperabilitu Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-215">Import the `qsharp` module, which registers the module loader for Q# interoperability.</span></span> 
    <span data-ttu-id="3fe5b-216">To umožňuje, aby se obory názvů Q # zobrazovaly jako moduly Pythonu, ze kterých můžeme "importovat" Q # volat.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-216">This allows Q# namespaces to appear as Python modules, from which we can "import" Q# callables.</span></span>
    <span data-ttu-id="3fe5b-217">Všimněte si, že se nejedná o vlastní volání Q #, která se naimportují, ale namísto zástupných procedur v Pythonu, které jim umožňují zavolat.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-217">Note that it is technically not the Q# callables themselves which are imported, but rather Python stubs which allow calling into them.</span></span>
    <span data-ttu-id="3fe5b-218">Ty se pak chovají jako objekty tříd Pythonu, na kterých používáme metody k určení cílových počítačů k odeslání operace k provedení.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-218">These then behave as objects of Python classes, on which we use methods to specify the target machines to send the operation to for execution.</span></span>

2. <span data-ttu-id="3fe5b-219">Naimportují se volání Q #, která v tomto případě budeme v tomto případě volat přímo--- `MeasureSuperposition` a `MeasureSuperpositionArray` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-219">Import those Q# callables which we will directly invoke---in this case, `MeasureSuperposition` and `MeasureSuperpositionArray`.</span></span>
    ```python
    import qsharp
    from NamespaceName import MeasureSuperposition, MeasureSuperpositionArray
    ```
    <span data-ttu-id="3fe5b-220">Pomocí `qsharp` importovaného modulu můžete také naimportovat volatelné přímo z oboru názvů knihovny Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-220">With the `qsharp` module imported, you can also import callables directly from the Q# library namespaces.</span></span>

3. <span data-ttu-id="3fe5b-221">V jakémkoli jiném kódu Pythonu teď můžete zavolat tyto výzvy na konkrétní cílové počítače a přiřadit jejich návrat k proměnným (Pokud vrátí hodnotu) pro další použití.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-221">Among any other Python code, you can now call those callables on specific target machines, and assign their returns to variables (if they return a value) for further use.</span></span>

#### <a name="specifying-target-machines"></a><span data-ttu-id="3fe5b-222">Určení cílových počítačů</span><span class="sxs-lookup"><span data-stu-id="3fe5b-222">Specifying target machines</span></span>
<span data-ttu-id="3fe5b-223">Volání operace, která se má spustit na konkrétním cílovém počítači, se provádí prostřednictvím různých metod Pythonu u importovaného objektu.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-223">Calling an operation to be run on a specific target machine is done via different Python methods on the imported object.</span></span>
<span data-ttu-id="3fe5b-224">Například `.simulate(<args>)` používá `QuantumSimulator` ke spuštění operace, zatímco `.estimate_resources(<args>)` to dělá na `ResourcesEstimator` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-224">For example, `.simulate(<args>)`, uses the `QuantumSimulator` to run the operation, whereas `.estimate_resources(<args>)` does so on the `ResourcesEstimator`.</span></span>

#### <a name="passing-inputs-to-q"></a><span data-ttu-id="3fe5b-225">Předání vstupů do Q\#</span><span class="sxs-lookup"><span data-stu-id="3fe5b-225">Passing inputs to Q\#</span></span>
<span data-ttu-id="3fe5b-226">Argumenty pro parametr Q # volat by měly být zadány ve formě argumentu klíčového slova, kde klíčové slovo je název argumentu v definici Q # volat.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-226">Arguments for the Q# callable should be provided in the form of a keyword argument, where the keyword is the argument name in the Q# callable definition.</span></span>
<span data-ttu-id="3fe5b-227">To znamená, že `MeasureSuperpositionArray.simulate(n=4)` je platná, zatímco `MeasureSuperpositionArray.simulate(4)` by vyvolala chybu.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-227">That is, `MeasureSuperpositionArray.simulate(n=4)` is valid, whereas `MeasureSuperpositionArray.simulate(4)` would throw an error.</span></span>

<span data-ttu-id="3fe5b-228">Proto hostitelský program Pythonu</span><span class="sxs-lookup"><span data-stu-id="3fe5b-228">Therefore, the Python host program</span></span> 

```python
import qsharp
from NamespaceName import MeasureSuperposition, MeasureSuperpositionArray

single_qubit_result = MeasureSuperposition.simulate()
single_qubit_resources = MeasureSuperposition.estimate_resources()

multi_qubit_result = MeasureSuperpositionArray.simulate(n=4)
multi_qubit_resources = MeasureSuperpositionArray.estimate_resources(n=4)

print('Single qubit:\n' + str(single_qubit_result))
print(single_qubit_resources)

print('\nMultiple qubits:\n' + str(multi_qubit_result))
print(multi_qubit_resources)
```

<span data-ttu-id="3fe5b-229">Výsledkem bude výstup podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-229">results in an output like the following:</span></span>

```python
Single qubit:
1
{'CNOT': 0, 'QubitClifford': 1, 'R': 0, 'Measure': 1, 'T': 0, 'Depth': 0, 'Width': 1, 'BorrowedWidth': 0}

Multiple qubits:
[0, 1, 1, 1]
{'CNOT': 0, 'QubitClifford': 4, 'R': 0, 'Measure': 4, 'T': 0, 'Depth': 0, 'Width': 4, 'BorrowedWidth': 0}
```

### <a name="c"></a>[<span data-ttu-id="3fe5b-230">C#</span><span class="sxs-lookup"><span data-stu-id="3fe5b-230">C#</span></span>](#tab/tabid-csharp)

<span data-ttu-id="3fe5b-231">Hostitelský program v jazyce C# má více komponent a pracuje velmi pečlivě s některými komponentami QDK, jako jsou například simulátory, které jsou samy postaveny na C#.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-231">A C# host program has multiple components, and works very closely with some components of the QDK, such as the simulators, which are themselves built on C#.</span></span>

<span data-ttu-id="3fe5b-232">Kompilátor Q # zde funguje tak, že generuje ekvivalentně pojmenovaný obor názvů jazyka C# z oboru názvů Q # v našem souboru Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-232">The Q# compiler works here by generating an equivalently named C# namespace from the Q# namespace in our Q# file.</span></span>
<span data-ttu-id="3fe5b-233">Dále vygeneruje ekvivalentní název třídy jazyka C# pro každé volání nebo typy, které jsou definovány v jazyce Q.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-233">It further generates an equivalently named C# class for each of the Q# callables or types defined therein.</span></span>

<span data-ttu-id="3fe5b-234">Nejprve zpřístupníme všechny třídy, které jsou v našem hostitelském programu k dispozici s `using` příkazy, které jsou zhruba analagous na `open` příkazy v našem souboru Q #:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-234">First, we make any classes used in our host program available with `using` statements, which are roughly analagous to the `open` statements in our Q# file:</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Quantum.Simulation.Simulators;    // contains the target machines (e.g. QuantumSimulator, ResourcesEstimator)
using NamespaceName;                              // make the Q# namespace available
```

<span data-ttu-id="3fe5b-235">Dále deklarujeme náš obor názvů C#, několik dalších bitů a částí (viz úplný blok kódu níže) a pak jakékoli klasické programování, které bychom chtěli (například výpočetní argumenty pro volat pro Q #).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-235">Next, we declare our C# namespace, a few other bits and pieces (see the full code block below), and then any classical programming we would like (e.g. computing arguments for the Q# callables).</span></span>
<span data-ttu-id="3fe5b-236">Ta není v našem případě nutná, ale příklad takového použití najdete v [ukázce interoperability .NET](https://github.com/microsoft/Quantum/tree/master/samples/interoperability/dotnet).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-236">The latter isn't necessary in our case, but an example of such usage can be found at the  [.NET interoperability sample](https://github.com/microsoft/Quantum/tree/master/samples/interoperability/dotnet).</span></span>

#### <a name="target-machines"></a><span data-ttu-id="3fe5b-237">Cílové počítače</span><span class="sxs-lookup"><span data-stu-id="3fe5b-237">Target machines</span></span>

<span data-ttu-id="3fe5b-238">Když se vrátíte zpět k verzi Q #, musíme vytvořit instanci libovolného cílového počítače, na které budeme provádět operace.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-238">Getting back to Q#, we must create an instance of whatever target machine we will execute our operations on.</span></span>

```csharp
            using var sim = new QuantumSimulator();
```

<span data-ttu-id="3fe5b-239">Použití jiných cílových počítačů je stejně jednoduché jako vytvoření instance jiného, přestože způsob, jak to udělat, a zpracování vrácených změn může být mírně odlišné.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-239">Using other target machines is as simple as instantiating a different one, although the manner of doing so and processing the returns can be slightly different.</span></span>
<span data-ttu-id="3fe5b-240">V případě zkrácení se [`QuantumSimulator`](xref:microsoft.quantum.machines.full-state-simulator) pro teď používáme a zařadíme [`ResourcesEstimator`](xref:microsoft.quantum.machines.resources-estimator) [níže](#including-the-resources-estimator).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-240">For brevity, we stick to the [`QuantumSimulator`](xref:microsoft.quantum.machines.full-state-simulator) for now, and include the [`ResourcesEstimator`](xref:microsoft.quantum.machines.resources-estimator) [below](#including-the-resources-estimator).</span></span>

<span data-ttu-id="3fe5b-241">Každá třída jazyka C# vygenerovaná z operací Q # má `Run` metodu, jejímž prvním argumentem musí být instance cílového počítače.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-241">Each C# class generated from the Q# operations have a `Run` method, the first argument of which must be the target machine instance.</span></span>
<span data-ttu-id="3fe5b-242">Takže pokud chcete spustit `MeasureSuperposition` v `QuantumSimulator` , používáme `MeasureSuperposition.Run(sim)` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-242">So, to run `MeasureSuperposition` on the `QuantumSimulator`, we use `MeasureSuperposition.Run(sim)`.</span></span>
<span data-ttu-id="3fe5b-243">Vrácené výsledky lze následně přiřadit proměnným v jazyce C#:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-243">The returned results can then be assigned to variables in C#:</span></span>

```csharp
            var singleQubitResult = await MeasureSuperposition.Run(sim);
```

> [!NOTE]
> <span data-ttu-id="3fe5b-244">`Run`Metoda je prováděna asynchronně, protože se jedná o případ reálného hardwaru s `await` více jádry, a proto klíčové slovo zablokuje další provádění až do dokončení úkolu.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-244">The `Run` method is executed asynchronously because this will be the case for real quantum hardware, and therefore the `await` keyword blocks further execution until the task completes.</span></span>

<span data-ttu-id="3fe5b-245">Pokud funkce Q # volat neobsahuje žádné vratky (tj. má návratový typ `Unit` ), může být provádění stále provedeno stejným způsobem bez přiřazení k proměnné.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-245">If the Q# callable does not have any returns (i.e. has return type `Unit`), then the execution can still be done in the same manner without assigning it to a variable.</span></span>
<span data-ttu-id="3fe5b-246">V takovém případě by se celý řádek měl jednoduše skládat z</span><span class="sxs-lookup"><span data-stu-id="3fe5b-246">In that case, the entire line would simply consist of</span></span> 
```csharp
await <callable>.Run(<simulator>);
```

#### <a name="arguments"></a><span data-ttu-id="3fe5b-247">Arguments</span><span class="sxs-lookup"><span data-stu-id="3fe5b-247">Arguments</span></span>

<span data-ttu-id="3fe5b-248">Jakékoli argumenty pro volat v Q # jsou jednoduše předány jako další argumenty grafice cílový počítač.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-248">Any arguments to the Q# callable are simply passed as additional arguments afer the target machine.</span></span>
<span data-ttu-id="3fe5b-249">Proto výsledky z `MeasureSuperpositionArray` `n=4` qubits by se načetly prostřednictvím</span><span class="sxs-lookup"><span data-stu-id="3fe5b-249">Hence the results of `MeasureSuperpositionArray` on `n=4` qubits would fetched via</span></span> 

```csharp
            var multiQubitResult = await MeasureSuperpositionArray.Run(sim, 4);
```

<span data-ttu-id="3fe5b-250">Úplný hostitelský program v C# by mohl vypadat takto</span><span class="sxs-lookup"><span data-stu-id="3fe5b-250">A full C# host program could thus look like</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Quantum.Simulation.Simulators;
using NamespaceName;

namespace host
{
    static class Program
    {
        static async Task Main(string[] args)
        {
            using var sim = new QuantumSimulator();

            var singleQubitResult = await MeasureSuperposition.Run(sim);
            var multiQubitResult = await MeasureSuperpositionArray.Run(sim, 4);

            Console.WriteLine($"Single qubit result: {singleQubitResult}");
            Console.WriteLine($"Multiple qubit result: {multiQubitResult}");
        }
    }
}
```

<span data-ttu-id="3fe5b-251">V umístění souboru jazyka C# lze hostitelský program spustit z příkazového řádku zadáním</span><span class="sxs-lookup"><span data-stu-id="3fe5b-251">At the location of the C# file, the host program can be run from the command line by entering</span></span>
```dotnetcli
dotnet run
```
<span data-ttu-id="3fe5b-252">v tomto případě se zobrazí výstup napsaný do konzoly podobně jako</span><span class="sxs-lookup"><span data-stu-id="3fe5b-252">and in this case you will see output written to the console similar to</span></span> 
```output
Single qubit result: One
Multiple qubit result: [One,One,Zero,Zero]
```

> [!NOTE]
> <span data-ttu-id="3fe5b-253">S ohledem na interoperabilitu kompilátoru s obory názvů můžeme Alternativně zpřístupnit naši adresu Q #, která je k dispozici bez `using NamespaceName;` příkazu, a jednoduše odpovídat názvu oboru názvů C#.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-253">Due to the compiler's interoperability with namespaces, we could alternatively make our Q# callables available without the `using NamespaceName;` statement, and simply matching the C# namespace title to it.</span></span>
> <span data-ttu-id="3fe5b-254">To znamená nahrazením `namespace host` pomocí `namespace NamespaceName` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-254">That is, by replacing `namespace host` with `namespace NamespaceName`.</span></span>

#### <a name="including-the-resources-estimator"></a><span data-ttu-id="3fe5b-255">Zahrnutí prostředků Estimator</span><span class="sxs-lookup"><span data-stu-id="3fe5b-255">Including the resources estimator</span></span>

<span data-ttu-id="3fe5b-256">[`ResourcesEstimator`](xref:microsoft.quantum.machines.resources-estimator)Pro načtení výstupu vyžaduje poněkud odlišnou implementaci.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-256">The [`ResourcesEstimator`](xref:microsoft.quantum.machines.resources-estimator) requires a slightly different implementation to retrieve the output.</span></span>

<span data-ttu-id="3fe5b-257">Nejprve místo toho, aby se vytvořila instance jako proměnná s `using` příkazem (stejně jako v případě `QuantumSimulator` ), je více přímo vytvořena instance objektů třídy prostřednictvím</span><span class="sxs-lookup"><span data-stu-id="3fe5b-257">Firstly, instead of instantiating them as a variable with a `using` statement (as we do with the `QuantumSimulator`), we more directly instantiate objects of the class via</span></span>

```csharp
            var estimatorSingleQ = new ResourcesEstimator();
            var estimatorMultiQ = new ResourcesEstimator();
```

<span data-ttu-id="3fe5b-258">Všimněte si, že místo jednoho cílového simulátoru, který má být použit více operacemi Q #, byl pro každou instanci vytvořen jeden.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-258">Notice that instead of a single target simulator to be used by multiple Q# operations, we have instantiated one for each.</span></span> <span data-ttu-id="3fe5b-259">Důvodem je to, že při použití jako cílové počítače jsou změněny samotné objekty a jejich výsledky lze následně načíst pomocí metody třídy `.ToTSV()` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-259">This is because the objects themselves are modified when used as target machines, and their results can then be retrieved afterwards with the class method `.ToTSV()`.</span></span>

<span data-ttu-id="3fe5b-260">Pro spuštění operací na odhady prostředků používáme</span><span class="sxs-lookup"><span data-stu-id="3fe5b-260">To run the operations on the resource estimators, we use</span></span>

```csharp
            await MeasureSuperposition.Run(estimatorSingleQ);
            await MeasureSuperpositionArray.Run(estimatorMultiQ, 4);
```
<span data-ttu-id="3fe5b-261">a potom výsledky načtěte jako hodnoty hodnot TSV (tabulátor-revalues) s `estimatorSingleQ.ToTSV()` a `estimatorMultiQ.ToTSV()` .</span><span class="sxs-lookup"><span data-stu-id="3fe5b-261">and then fetch the results as tab-separated-values (TSV) with `estimatorSingleQ.ToTSV()` and `estimatorMultiQ.ToTSV()`.</span></span>

<span data-ttu-id="3fe5b-262">Úplný hostitelský program v jazyce C#, který používá jak `QuantumSimulator` a `ResourcesEstimator` může mít podobu:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-262">So, a full C# host program making use of both the `QuantumSimulator` and `ResourcesEstimator` could take the form:</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Quantum.Simulation.Simulators;
using NamespaceName;

namespace host
{
    static class Program
    {
        static async Task Main(string[] args)
        {
            using var sim = new QuantumSimulator();
            var estimatorSingleQ = new ResourcesEstimator();
            var estimatorMultiQ = new ResourcesEstimator();

            var singleQubitResult = await MeasureSuperposition.Run(sim);
            var multiQubitResult = await MeasureSuperpositionArray.Run(sim, 4);

            await MeasureSuperposition.Run(estimatorSingleQ);
            await MeasureSuperpositionArray.Run(estimatorMultiQ, 4);

            Console.WriteLine($"Single qubit result: {singleQubitResult}");
            Console.WriteLine("Single qubit resources:");
            Console.WriteLine(estimatorSingleQ.ToTSV());

            Console.WriteLine($"\nMultiple qubit result: {multiQubitResult}");
            Console.WriteLine("Multiple qubit resources:");
            Console.WriteLine(estimatorMultiQ.ToTSV());
        }
    }
}
```


<span data-ttu-id="3fe5b-263">což by znamenalo výstup podobný</span><span class="sxs-lookup"><span data-stu-id="3fe5b-263">which would yield output similar to</span></span>

```output
Single qubit result: One
Single qubit resources:
Metric          Sum
CNOT            0
QubitClifford   1
R               0
Measure         1
T               0
Depth           0
Width           1
BorrowedWidth   0

Multiple qubit result: [One,One,One,Zero]
Multiple qubit resources:
Metric          Sum
CNOT            0
QubitClifford   4
R               0
Measure         4
T               0
Depth           0
Width           4
BorrowedWidth   0
```

***

## <a name="q-jupyter-notebooks"></a><span data-ttu-id="3fe5b-264">Aplikace Jupyter Notebook v Q#</span><span class="sxs-lookup"><span data-stu-id="3fe5b-264">Q# Jupyter Notebooks</span></span>
<span data-ttu-id="3fe5b-265">Q # Jupyter poznámkové bloky využívají jádro SWEETIQ #, které umožňuje definovat, kompilovat a spouštět Q # volat v jednom poznámkovém bloku---všech společně s pokyny, poznámkami a dalšími obsahy.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-265">Q# Jupyter Notebooks make use of the IQ# kernel, which allows you to define, compile, and run Q# callables in a single notebook---all alongside instructions, notes, and other content.</span></span>
<span data-ttu-id="3fe5b-266">To znamená, že přestože je možné importovat a používat obsah `*.qs` souborů Q #, nejsou v modelu spuštění nutné.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-266">This means that while it is possible to import and use the contents of `*.qs` Q# files, they are not necessary in the execution model.</span></span>

<span data-ttu-id="3fe5b-267">Tady si podrobně podíváme, jak spustit výše uvedené operace Q #, ale v [úvodu do notebooků q # a Jupyter](https://github.com/microsoft/Quantum/blob/master/samples/getting-started/intro-to-iqsharp/Notebook.ipynb)je k dispozici širší Úvod k použití notebooků q # Jupyter.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-267">Here, we will detail how to run the Q# operations defined above, but a more broad introduction to using Q# Jupyter Notebooks is provided at [Intro to Q# and Jupyter Notebooks](https://github.com/microsoft/Quantum/blob/master/samples/getting-started/intro-to-iqsharp/Notebook.ipynb).</span></span>

### <a name="defining-operations"></a><span data-ttu-id="3fe5b-268">Definování operací</span><span class="sxs-lookup"><span data-stu-id="3fe5b-268">Defining operations</span></span>

<span data-ttu-id="3fe5b-269">V Jupyter Notebook Q # zadáte kód Q # stejně jako v rámci oboru názvů souboru Q #.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-269">In a Q# Jupyter Notebook, you enter Q# code just as we would from inside the namespace of a Q# file.</span></span>

<span data-ttu-id="3fe5b-270">Proto můžeme povolit přístup k volat z [standartní knihovny Q #](xref:microsoft.quantum.qsharplibintro) s `open` příkazy pro jejich příslušné obory názvů.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-270">So, we can enable access to callables from the [Q# standard libraries](xref:microsoft.quantum.qsharplibintro) with `open` statements for their respective namespaces.</span></span>
<span data-ttu-id="3fe5b-271">Po spuštění buňky s takovým příkazem jsou definice z těchto oborů názvů dostupné v celém pracovním prostoru.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-271">Upon running a cell with such a statement, the definitions from those namespaces are available throughout the workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="3fe5b-272">K operacím definovaným v [Microsoft.Quantum.Intrinsic](xref:microsoft.quantum.intrinsic) rámci buněk v [Microsoft.Quantum.Canon](xref:microsoft.quantum.canon) [`H`](xref:microsoft.quantum.intrinsic.h) [`ApplyToEach`](xref:microsoft.quantum.canon.applytoeach) poznámkových blocích Q # Jupyter se budou automaticky přivolat z Microsoft. probíhají. vnitřní a Microsoft.. Canon (např. a).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-272">Callables from [Microsoft.Quantum.Intrinsic](xref:microsoft.quantum.intrinsic) and [Microsoft.Quantum.Canon](xref:microsoft.quantum.canon) (e.g. [`H`](xref:microsoft.quantum.intrinsic.h) and [`ApplyToEach`](xref:microsoft.quantum.canon.applytoeach)) are automatically available to operations defined within cells in Q# Jupyter Notebooks.</span></span>
> <span data-ttu-id="3fe5b-273">To však není pravdivé pro kód, který je součástí z externích zdrojových souborů Q # (proces zobrazený v [úvodu do poznámkových bloků q # a Jupyter](https://github.com/microsoft/Quantum/blob/master/samples/getting-started/intro-to-iqsharp/Notebook.ipynb)).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-273">However, this is not true for code brought in from external Q# source files (a process shown at [Intro to Q# and Jupyter Notebooks](https://github.com/microsoft/Quantum/blob/master/samples/getting-started/intro-to-iqsharp/Notebook.ipynb)).</span></span> 
> 

<span data-ttu-id="3fe5b-274">Podobně definování operací vyžaduje pouze zápis kódu Q # a spuštění buňky.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-274">Similarly, defining operations requires only writing the Q# code and running the cell.</span></span>

<img src="../media/hostprograms_jupyter_op_def_crop.png" alt="Jupyter cell defining Q# operations" width="600">

<span data-ttu-id="3fe5b-275">Výstup pak obsahuje seznam operací, které je možné volat z budoucích buněk.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-275">The output then lists those operations, which can then be called from future cells.</span></span>

### <a name="target-machines"></a><span data-ttu-id="3fe5b-276">Cílové počítače</span><span class="sxs-lookup"><span data-stu-id="3fe5b-276">Target machines</span></span>

<span data-ttu-id="3fe5b-277">Funkce pro spouštění operací na konkrétních cílových počítačích se poskytuje prostřednictvím [příkazů sweetiq # Magic](xref:microsoft.quantum.guide.quickref.iqsharp).</span><span class="sxs-lookup"><span data-stu-id="3fe5b-277">The functionality to run operations on specific target machines is provided via [IQ# Magic Commands](xref:microsoft.quantum.guide.quickref.iqsharp).</span></span>
<span data-ttu-id="3fe5b-278">Například využívá `%simulate` `QuantumSimulator` a `%estimate` používá `ResourcesEstimator` :</span><span class="sxs-lookup"><span data-stu-id="3fe5b-278">For example, `%simulate` makes use of the `QuantumSimulator`, and `%estimate` uses the `ResourcesEstimator`:</span></span>

<img src="../media/hostprograms_jupyter_no_args_sim_est_crop.png" alt="Simulate and estimate resources Jupyter cell" width="500">

### <a name="passing-inputs-to-functions-and-operations"></a><span data-ttu-id="3fe5b-279">Předávání vstupů do funkcí a operací</span><span class="sxs-lookup"><span data-stu-id="3fe5b-279">Passing inputs to functions and operations</span></span>

<span data-ttu-id="3fe5b-280">V současné době se příkazy pro spuštění Magic dají použít jenom s operacemi, které nevyužívají žádné argumenty.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-280">Currently the execution magic commands can only be used with operations that take no arguments.</span></span> <span data-ttu-id="3fe5b-281">Takže aby bylo možné spustit `MeasureSuperpositionArray` , musíme definovat operaci "Obálka", která pak zavolá operaci s argumenty:</span><span class="sxs-lookup"><span data-stu-id="3fe5b-281">So, to run `MeasureSuperpositionArray`, we need to define a "wrapper" operation which then calls the operation with the arguments:</span></span>

<img src="../media/hostprograms_jupyter_wrapper_def_sim_crop.png" alt="Wrapper function and simulate Jupyter cell" width="550">

<span data-ttu-id="3fe5b-282">Tuto operaci je možné použít podobně jako v rámci `%estimate` a dalších příkazů pro spuštění.</span><span class="sxs-lookup"><span data-stu-id="3fe5b-282">This operation can of course be used similarly with `%estimate` and other execution commands.</span></span>