---
title: Movendo objetos de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], models
- data mining editor [Analysis Services]
- mining models [Analysis Services], managing
- Data Mining Designer
- mining models [Analysis Services], modifying
ms.assetid: bc108407-2603-4387-b930-b5bb9df78069
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a73a9b7fa99e42ff9846faafee6de5258e03ba7c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733374"
---
# <a name="moving-data-mining-objects"></a>Movendo objetos de mineração de dados
  Os cenários mais comuns para mover objetos de mineração de dados são implantar um modelo de um ambiente de teste ou análise para um ambiente de produção ou compartilhar modelos com outros usuários.  
  
 Este tópico descreve como você pode usar as ferramentas e as linguagens de scripts fornecidas pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], para mover objetos de mineração de dados.  
  
## <a name="moving-data-mining-objects-between-databases-or-servers"></a>Movendo objetos de mineração de dados entre bancos de dados ou servidores  
 Você pode mover objetos de mineração de dados entre os bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou entre instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das seguintes maneiras:  
  
-   Reimplantando a solução em um banco de dados diferente.  
  
-   Criando scripts de objetos individuais.  
  
-   Fazendo backup e restaurando uma cópia do banco de dados.  
  
-   Exportando e importando estruturas e modelos.  
  
 As seções a seguir explicam essas opções em mais detalhes.  
  
### <a name="deploying"></a>Implantando  
 Implantar a solução em um servidor ou banco de dados diferente exige que você tenha o arquivo de solução que foi criado usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Para obter mais informações sobre como implantar soluções do Analysis Services, consulte [Implantar projetos do Analysis Services &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
### <a name="scripting"></a>Script  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece vários idiomas que você pode usar para criar script de objetos.  
  
-   **XMLA**: Você pode criar scripts de objetos usando o XMLA clicando com o objetos em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para executar o script, abra-o na janela **Consulta XMLA** no servidor de destino.  
  
-   **DMX**: Você pode criar scripts usando modelos ou um dos construtores de consulta fornecidos no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Observe, no entanto, que há diferenças nas tarefas que você pode executar com cada linguagem de scripts:  
  
-   As propriedades como a descrição de objetos e as associações de dados só podem ser criadas ou alteradas usando as linguagens de DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , não usando DMX.  
  
-   Somente o DMX dá suporte à importação e exportação de objetos de mineração.  
  
-   Somente o DMX dá suporte à geração de PMML ou importação de definições de modelo de PMML.  
  
-   Somente o DMX dá suporte ao treinamento de um modelo com dados de aplicativo. Além disso, a instrução DMX INSERT INTO dá suporte a treinamento de um modelo sem fornecer valores para uma coluna de chave.  
  
 Para obter mais informações, consulte [Desenvolvendo com ASSL &#40;linguagem de script do Analysis Services&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
### <a name="backup-and-restore"></a>Backup e restauração  
 Backup e restauração de um banco de dados inteiro do Analysis Services é o método preferencial se a sua solução de mineração de dados utiliza objetos OLAP. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece a funcionalidade de backup e restauração que agiliza e simplifica os backups de banco de dados.  
  
 Para obter informações sobre o backup, consulte [Backup e restauração de Bancos de Dados do Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
### <a name="exporting-and-importing"></a>Exportando e importando  
 Exportar e, em seguida, reimportar os modelos e as estruturas de mineração usando instruções DMX é a maneira mais fácil de mover ou fazer backup de objetos de mineração de dados relacionais individuais. Para obter mais informações sobre a sintaxe DMX para essas operações, consulte os seguintes tópicos:  
  
-   [EXPORT &#40;DMX&#41;](/sql/dmx/export-dmx)  
  
-   [IMPORT &#40;DMX&#41;](/sql/dmx/import-dmx)  
  
 Se você especificar a opção INCLUDE DEPENDENCIES, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também exportará a definição de qualquer exibição da fonte de dados necessária e, quando você importar o modelo ou a estrutura, ele recriará a exibição da fonte de dados no servidor de destino. Depois que você terminar de importar o modelo, defina as permissões de mineração necessárias no objeto.  
  
> [!NOTE]  
>  Não é possível exportar e importar modelos OLAP usando DMX. Se o modelo de mineração se basear em um cubo OLAP, você deverá usar a funcionalidade fornecida pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para fazer backup e restauração de um banco de dados inteiro, ou reimplantar o cubo e seus modelos.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de soluções de mineração de dados e objetos](management-of-data-mining-solutions-and-objects.md)  
  
  
