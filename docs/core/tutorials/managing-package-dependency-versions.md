---
title: "Управление версиями зависимостей пакетов для .NET Core 1.0"
description: "Управление версиями зависимостей пакетов для .NET Core 1.0"
keywords: .NET, .NET Core
author: cartermp
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 4424a947-bdf9-4775-8d48-dc350a4e0aee
translationtype: Human Translation
ms.sourcegitcommit: dd32f1dd4d17ab1bb01b5578237cc950b147898c
ms.openlocfilehash: 676ffd19ac3e39b8260d626a81e9c1db8d58f19b

---

# <a name="how-to-manage-package-dependency-versions-for-net-core-10"></a>Управление версиями зависимостей пакетов для .NET Core 1.0

В этой статье приводятся необходимые сведения о версиях пакетов для библиотек и приложений .NET Core.

## <a name="glossary"></a>Глоссарий

**Исправление**. Под исправлением зависимостей понимается использование "семейства" пакетов, выпущенного в NuGet, для .NET Core 1.0.

**Метапакет** — пакет NuGet, представляющий набор пакетов NuGet.

**Усечение** — удаление пакетов, которые не используются, из метапакета.  Эта операция выполняется разработчиками пакетов NuGet.  Дополнительные сведения см. в разделе [Сокращение зависимостей пакетов с помощью файла project.json](../deploying/reducing-dependencies.md). 

## <a name="fix-your-dependencies-to-net-core-10"></a>Исправление зависимостей для .NET Core 1.0

Для надежного восстановления пакетов и написания надежного кода важно исправить зависимости до версий пакетов, поставляемых вместе с .NET Core 1.0.  Это означает, что каждый пакет должен иметь одну версию без дополнительных квалификаторов.

**Примеры пакетов, исправленных до версии 1.0**

`"System.Collections":"4.0.11"`

`"NETStandard.Library":"1.6.0"`

`"Microsoft.NETCore.App":"1.0.0"`

**Примеры пакетов, которые НЕ исправлены до версии 1.0**

`"Microsoft.NETCore.App":"1.0.0-rc4-00454-00"`

`"System.Net.Http":"4.1.0-*"`

`"System.Text.RegularExpressions":"4.0.10-rc3-24021-00"`

### <a name="why-does-this-matter"></a>Почему это важно

Мы гарантируем, что, если вы исправите зависимости до версий, поставляемых вместе с .NET Core 1.0, эти пакеты будут работать вместе.  При использовании пакетов ,которые не исправлены подобным образом, такой гарантии нет.

### <a name="scenarios"></a>Сценарии

Хотя список пакетов и их версий, выпускаемых с .NET Core 1.0, весьма велик, вам не придется изучать его полностью, если ваш код соответствует ряду условий.

**Используете ли вы только** `NETStandard.Library`**?**

Если да, пакет `NETStandard.Library` следует исправить до версии `1.6`.  Так как это проверенный метапакет, его оболочка также исправляется до версии 1.0.

**Используете ли вы только** `Microsoft.NETCore.App`**?**

Если да, пакет `Microsoft.NETCore.App` следует исправить до версии `1.0.0`.  Так как это проверенный метапакет, его оболочка также исправляется до версии 1.0.

**[Усекаете](../deploying/reducing-dependencies.md) ли вы зависимости метапакета** `NETStandard.Library` **или** `Microsoft.NETCore.App`**?**

Если да, то используемый метапакет должен быть исправлен до версии 1.0.  Отдельные пакеты, которые вы используете после усечения, также исправляются до версии 1.0.

**Используются ли пакеты вне метапакета** `NETStandard.Library` **или** `Microsoft.NETCore.App`**?**

Если да, необходимо исправить остальные зависимости до версии 1.0.  Правильные версии пакетов и номера сборок см. в конце этой статьи.

### <a name="a-note-on-using-a-splat-string-when-versioning"></a>Замечание об использовании строки со звездочкой (\*) при управлении версиями

Возможно, вы применяете шаблон управления версиями, предусматривающий использование строки со звездочкой (\*) наподобие следующей: `"System.Collections":"4.0.11-*"`.

**Этого не следует делать**.  Использование строки со звездочкой может привести к восстановлению пакетов из разных сборок, некоторые из которых могут быть более поздними, чем выпускаемые с .NET Core 1.0.  Это, в свою очередь, может привести к несовместимости некоторых пакетов.

## <a name="packages-and-version-numbers-organized-by-metapackage"></a>Пакеты и номера версий по метапакетам

[Список всех пакетов библиотеки .NET Standard и их версий для 1.0](https://github.com/dotnet/versions/blob/master/build-info/dotnet/corefx/release/1.0.0/Latest_Packages.txt).

[Список всех пакетов среды выполнения и их версий для 1.0](https://github.com/dotnet/versions/blob/master/build-info/dotnet/coreclr/release/1.0.0/LKG_Packages.txt).

[Список всех пакетов приложений .NET Core и их версий для 1.0](https://github.com/dotnet/versions/blob/master/build-info/dotnet/core-setup/release/1.0.0/Latest_Packages.txt).



<!--HONumber=Nov16_HO3-->

