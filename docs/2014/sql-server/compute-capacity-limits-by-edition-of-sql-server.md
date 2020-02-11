---
title: Computar limites de capacidade por edição do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- processors [SQL Server], supported
- number of processors supported
- maximum number of processors supported
ms.assetid: cd308bc9-9468-40cc-ad6e-1a8a69aca6c8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f457c901c4226b9a0ead23de57c2455c619f406e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62714754"
---
# <a name="compute-capacity-limits-by-edition-of-sql-server"></a>Computar limites de capacidade por edição do SQL Server
  Esse tópico discute os limites de capacidade de computação para edições diferentes do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e como elas podem diferir em ambientes físicos e virtualizados com processadores hyper-threaded.  
  
 ![Mapeamentos para calcular limites de capacidade](../../2014/getting-started/media/compute-capacity-limits.gif "Mapeamentos para calcular limites de capacidade")  
  
 A tabela a seguir descreve as notações que são usadas no diagrama acima:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|0..1|Zero ou um|  
|1|Exatamente um|  
|1..*|Um ou mais|  
|0..*|Zero ou mais|  
|1..2|Um ou dois|  
  
> [!IMPORTANT]
>  Para elaborar mais:  
> 
>  1.  Uma máquina virtual é alocada um ou mais processadores virtuais.  
> 2.  Uma ou mais processadores virtuais são alocados a exatamente uma máquina virtual.  
> 3.  Zero ou um processador virtual é mapeado para zero ou mais processadores lógicos. Quando o mapeamento do processador virtual para o processador lógico é:  
> 
>      -   Um para zero representa um processador lógico não associado não usado pelos sistemas operacionais convidados.  
>     -   Um para muitos representa uma superconfirmação.  
>     -   Zero para muitos representa a ausência de máquina virtual no sistema host, de modo que nenhum processador lógico seja usado por máquinas virtuais.  
> 4.  Um soquete é mapeado para zero ou mais núcleos. Quando o soquete para o mapeamento de núcleo é:  
> 
>      -   Um para zero representa um soquete vazio (nenhum chip instalado).  
>     -   Um para um representa um chip de núcleo único instalado no soquete (muito raro estes dias).  
>     -   Um para muitos representa um chip de núcleo múltiplo instalado no soquete (os valores típicos são 2,4,8).  
> 5.  Um núcleo é mapeado para um ou dois processadores lógicos. Quando o mapeamento do núcleo para o processador lógico é:  
> 
>      -   O hyperthreading de um para um está desativado.  
>     -   O hyperthreading de um para dois está ativado.  
  
 As definições a seguir se aplicam às condições usadas ao longo deste tópico:  
  
-   Um thread ou processador lógico é um mecanismo de computação lógico da perspectiva do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o sistema operacional, um aplicativo ou driver.  
  
-   Um núcleo é uma unidade de processador que pode consistir em um ou mais processadores lógicos.  
  
-   Um processador físico pode consistir em um ou mais núcleos. Um processador físico é o mesmo que um pacote de processador ou um soquete.  
  
 Os sistemas com mais de um processador físico ou sistemas com processadores físicos que têm vários núcleos e/ou hyperthreads permitem que o sistema operacional execute várias tarefas simultaneamente. Cada thread de execução aparece como um processador lógico. Por exemplo, se você tiver um computador com dois processadores com núcleo quad com hyper-threading habilitado e dois threads por núcleo, terá 16 processadores lógicos: 2 processadores x 4 núcleos por processador x 2 threads por núcleo. Vale observar que:  
  
-   A capacidade de computação de um processador lógico de um único thread de um núcleo hyper-threaded é menor que a capacidade de computação de um processador lógico daquele mesmo núcleo com hyperthreading desabilitado.  
  
-   Mas a capacidade de computação dos 2 processadores lógicos no núcleo hyper-threaded é maior que a capacidade de computação do mesmo núcleo com hyperthreading desabilitado.  
  
 Cada edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem dois limites de capacidade de computação:  
  
1.  Um número máximo de soquetes (o mesmo que o processador físico ou soquete ou pacote de processador).  
  
2.  Um número máximo de núcleos como relatado pelo sistema operacional.  
  
 Esses limites se aplicam a uma única instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Eles representam a capacidade máxima de computação que uma única instância usará. Eles não restringem o servidor no qual a instância pode ser implantada. De fato, implantar várias instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no mesmo servidor físico é um modo eficiente de usar a capacidade de computação de um servidor físico com mais soquetes e/ou núcleos que os limites de capacidade a seguir.  
  
 A tabela a seguir especifica os limites de capacidade de computação para uma única instância de cada edição do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]:  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Versão|Capacidade máxima de computação usada por uma única instância ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)])|Capacidade máxima de computação usada por uma única instância (AS, RS)|  
|---------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
|Enterprise Edition: licenciamento baseado em núcleo<sup>1</sup>|Máximo do sistema operacional|Máximo do sistema operacional|  
|Desenvolvedor|Máximo do sistema operacional|Máximo do sistema operacional|  
|Avaliação|Máximo do sistema operacional|Máximo do sistema operacional|  
|Business Intelligence|Limitado a menos de 4 soquetes ou 16 núcleos|Máximo do sistema operacional|  
|Standard|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|  
|Web|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|  
|Express|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|  
|Express with Tools|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|  
|Express with Advanced Services|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|  
  
 <sup>1</sup> Enterprise Edition com servidor + licenciamento baseado em Cal (licença de acesso para cliente) (não disponível para novos contratos) é limitado a um máximo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 20 núcleos por instância. Não há limites no modelo de Licenciamento de Servidor Baseado em Núcleo.  
  
 Em um ambiente virtualizado, o limite da capacidade de computação é baseado no número de processadores lógicos, não núcleos, porque a arquitetura de processador não é visível aos aplicativos convidados.  Por exemplo, um servidor com quatro soquetes populados com processadores com núcleo quad e a capacidade para habilitar dois hyperthreads por núcleo contém 32 processadores lógicos com hyperthreading habilitado, mas só 16 processadores lógicos com hyperthreading desabilitado. Esses processadores lógicos podem ser mapeados para máquinas virtuais no servidor com a carga de computação das máquinas virtuais nesse processador lógico mapeado em um thread de execução no processador físico no servidor host.  
  
 Você poderá querer desabilitar hyperthreading quando o desempenho por processador virtual for importante. A pessoa pode habilitar ou desabilitar hyperthreading usando uma configuração de BIOS para o processador durante a instalação da BIOS, mas é geralmente uma operação no escopo do servidor, que afetará todas as cargas de trabalho que estão sendo executadas no servidor. Isto pode sugerir separar cargas de trabalho que serão executadas em ambientes virtualizados dos que se beneficiariam do aumento de desempenho de hyperthreading em um ambiente de sistema operacional físico.  
  
## <a name="see-also"></a>Consulte Também  
 [Edições e componentes do SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Recursos com suporte nas edições do SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Especificações de capacidade máxima para SQL Server](../sql-server/maximum-capacity-specifications-for-sql-server.md)   
 [Instalação de início rápido do SQL Server 2014](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
