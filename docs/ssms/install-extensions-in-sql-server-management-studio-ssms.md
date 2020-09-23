---
description: Instalar as extensões no SSMS (SQL Server Management Studio)
title: Instalar as extensões no SSMS (SQL Server Management Studio)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
keywords:
- extensions
- vsix
- instalar extensão
- instalar vsix
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 07/29/2020
ms.openlocfilehash: bf4c9ee5287a2e0fdecf8455334561ce130499bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492020"
---
# <a name="install-extensions-in-sql-server-management-studio-ssms"></a>Instalar as extensões no SSMS (SQL Server Management Studio)

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

As extensões do SSMS (SQL Server Management Studio) são criadas com C# por meio da carga de trabalho "Desenvolvimento de extensão do Visual Studio" no Visual Studio. O SSMS 18.x foi criado no shell do Visual Studio 2017 e está sujeito às limitações desse ambiente.

A instalação da extensão no SSMS 18.x pode ser obtida com a implantação do VSIX por meio do Visual Studio ou de um instalador de pacote gerenciado independente.  A implantação do Visual Studio é descrita abaixo.

> [!NOTE]
> As extensões do SQL Server Management Studio não podem ser instaladas por meio do VSIXInstaller no SSMS 18.x.
  
## <a name="visual-studio-deployment-of-an-extension-for-ssms-18x"></a>Implantação do Visual Studio de uma extensão para SSMS 18.x

A instalação da extensão manual é realizada com a cópia dos arquivos de extensão associados (VSIX) na pasta das extensões de SSMS padrão.  O SSMS verifica automaticamente essa pasta em busca de extensões na inicialização.  A implantação do VSIX pode ser concluída pelo Visual Studio no momento do build do projeto. 

  
1.  Localize sua instalação do SSMS e a pasta de extensões padrão.  Com as configurações de instalação padrão do SSMS, o local da pasta é ```C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\Extensions\```.  


2. Inicie o Visual Studio como administrador.

3.  O processo de cópia de arquivo pode ser concluído pelo Visual Studio no momento do build marcando a caixa de seleção "Copiar conteúdo do VSIX para o seguinte local" na guia VSIX da janela de propriedades do projeto. Na caixa de texto abaixo da caixa de seleção, insira o local da pasta acima com uma pasta para essa extensão acrescentada.  Por exemplo: ```C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\Extensions\SampleExtension```
  
![Configurações VSIX da janela de propriedades do projeto com três caixas de seleção e uma caixa de texto](./media/install-extensions/vsix_ssms.png)

4. Compile o projeto de extensão. Um build bem-sucedido transferirá os arquivos de extensão para a pasta de extensão do SSMS.

5.  Inicie o SSMS e teste a funcionalidade da extensão.
  
