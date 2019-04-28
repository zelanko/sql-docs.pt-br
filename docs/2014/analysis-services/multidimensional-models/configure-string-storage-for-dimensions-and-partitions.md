---
title: Configurar o armazenamento de cadeia de caracteres para dimensões e partições | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 987f6cfc-da82-4b2e-96ef-a8af88339e5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 29f5e6952c733ac56671e48fd1ec809b3f0ab329
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62700923"
---
# <a name="configure-string-storage-for-dimensions-and-partitions"></a>Configurar o armazenamento de cadeia de caracteres para dimensões e partições
  Você pode reconfigurar o armazenamento de cadeia de caracteres para acomodar cadeias de caracteres muito grandes em atributos de dimensão ou partições que excedem o limite de tamanho de arquivo do 4 GB para repositórios de cadeias de caracteres. Se suas dimensões ou partições incluírem repositórios de cadeias de caracteres desse tamanho, você poderá contornar a restrição de tamanho do arquivo alterando a propriedade **StringStoresCompatibilityLevel** em nível de dimensão ou de partição para objetos locais e vinculados (locais ou remotos).  
  
 Observe que você pode aumentar o armazenamento de cadeia de caracteres apenas nos objetos que exigem capacidade adicional. Na maioria dos modelos multidimensionais, os dados de cadeia de caracteres são associados às dimensões. No entanto, partições que contêm medidas de contagem distintas sobre cadeias de caracteres também podem aproveitar essa configuração. Como a configuração é para cadeias de caracteres, dados numéricos não são afetados.  
  
 Os valores válidos para essa propriedade incluem os seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1050**|Especifica a arquitetura de armazenamento de cadeias de caracteres padrão, sujeita a um tamanho de arquivo máximo de 4 GB por repositório.|  
|**1100**|Especifica um maior armazenamento de cadeias de caracteres, dá suporte a até quatro bilhões de cadeias de caracteres exclusivas por repositório.|  
  
> [!IMPORTANT]  
>  A alteração das configurações do armazenamento de cadeias de caracteres de um objeto requer que você reprocesse próprio objeto e qualquer objeto dependente. O processamento é necessário para concluir o procedimento.  
  
 Este tópico contém as seguintes seções:  
  
-   [Sobre repositórios de cadeias de caracteres](#bkmk_background)  
  
-   [Pré-requisitos](#bkmk_prereq)  
  
-   [Etapa 1: Definir a propriedade StringStoreCompatiblityLevel no SQL Server Data Tools](#bkmk_step1)  
  
-   [Etapa 2: Os objetos de processo](#bkmk_step2)  
  
##  <a name="bkmk_background"></a> Sobre repositórios de cadeias de caracteres  
 A configuração do armazenamento de cadeias de caracteres é opcional, o que significa que até mesmo novos bancos de dados criados usam a arquitetura de repositório de cadeias de caracteres padrão que está sujeita ao tamanho de arquivo máximo de 4 GB. O uso de uma maior arquitetura de armazenamento de cadeia de caracteres tem um impacto pequeno mas notável no desempenho. Você deve usá-la apenas se seus arquivos de armazenamento de cadeias de caracteres estiverem próximos ou no limite máximo de 4 GB.  
  
> [!NOTE]  
>  Essa configuração não se aplica a modelos de mineração de dados. No momento, ainda é possível localizar a limitação de tamanho de arquivo GB em modelos que contenham estruturas de mineração de dados.  
  
 Em um banco de dados multidimensional do Analysis Services, as cadeias de caracteres são armazenadas separadamente dos dados numéricos para permitir otimizações baseadas nas características dos dados. Dados de cadeia de caracteres normalmente são localizados em atributos de dimensão que representam nomes ou descrições. Também é possível ter dados de cadeia de caracteres em medidas de contagens distintas. Os dados de cadeia de caracteres também podem ser usados em chaves.  
  
 Você pode identificar um repositório de cadeias de caracteres por sua extensão de arquivo (por exemplo, arquivos asstore, .bstore, .ksstore ou .string). Por padrão, cada um desses arquivos está sujeito a um limite máximo de 4 GB. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], é possível substituir o tamanho máximo do arquivo especificando um mecanismo de armazenamento alternativo que permite que um repositório de cadeias de caracteres cresça conforme necessário.  
  
 Em comparação com a arquitetura de armazenamento de cadeias de caracteres padrão que limita o tamanho do arquivo físico, um maior armazenamento de cadeias de caracteres é baseado em um número máximo de cadeias de caracteres. O limite máximo para um maior armazenamento de cadeias de caracteres é de quatro bilhões de cadeias de caracteres exclusivas ou quatro bilhões de registros, o que ocorrer primeiro. Um maior armazenamento de cadeias de caracteres cria registros de um tamanho uniforme, em que cada registro é igual a uma página de 64 K. Se você tiver cadeias de caracteres muito longas que não se ajustem em um único registro, seu limite efetivo será menor do que quatro bilhões de cadeias de caracteres.  
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
 Você deve ter uma versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou posterior do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Dimensões e partições devem usar o armazenamento MOLAP  
  
 O nível de compatibilidade do banco de dados deve ser definido como 1100. Se você criar ou implantar um banco de dados usando o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] e o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou uma versão posterior do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o nível de compatibilidade do banco de dados já estará definido como 1100. Se você mover um banco de dados criado em uma versão anterior do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o ssSQL11 ou posterior, deverá atualizar o nível de compatibilidade. Para bancos de dados que você está movendo, mas não reimplantando, você poderá usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para definir o nível de compatibilidade. Para obter mais informações, consulte [definir o nível de compatibilidade de um banco de dados Multidimensional &#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
##  <a name="bkmk_step1"></a> Etapa 1: Definir a propriedade StringStoreCompatiblityLevel no SQL Server Data Tools  
  
1.  Usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto que contém as dimensões ou as partições que você deseja modificar.  
  
2.  Para alterar o armazenamento de cadeia de caracteres para dimensões, abra o Gerenciador de Soluções. Clique duas vezes na dimensão para a qual você está modificando o armazenamento de cadeias de caracteres.  
  
3.  No Designer de Dimensão, no painel Atributos, verifique se o nó pai da dimensão está selecionado (por exemplo, se a dimensão for Clientes, selecione Clientes e não um dos atributos filho).  
  
4.  No painel Propriedades, na seção Avançado, defina **StringStoresCompatibilityLevel** como **1100**. Repita o procedimento para outras dimensões que exigem um armazenamento maior, caso contrário, deixe as dimensões restantes com o valor **1050** .  
  
5.  Para partições, abra um cubo no Gerenciador de Soluções.  
  
6.  Clique na guia Partições.  
  
7.  Expanda a partição, selecione a partição que exige capacidade de armazenamento adicional e modifique a propriedade **StringStoresCompatibilityLevel** .  
  
8.  Salve o arquivo.  
  
##  <a name="bkmk_step2"></a> Etapa 2: Os objetos de processo  
 A nova arquitetura de armazenamento será usada depois que você processar os objetos. O processamento dos objetos também prova que você resolveu o problema de restrição de armazenamento com êxito porque o erro que relatava uma condição de estouro do repositório de cadeias de caracteres não deve mais ocorrer.  
  
-   No Gerenciador de Soluções, clique com o botão direito do mouse na dimensão que você acabou de modificar e selecione **Processar**.  
  
 Você deve usar a opção Processar Completo em cada objeto que esteja usando a nova arquitetura de repositório de cadeias de caracteres. Antes de processar, execute uma análise de impacto na dimensão para verificar se objetos dependentes também requerem reprocessamento.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas e abordagens para processamento &#40;Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md)   
 [Processando opções e configurações &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md)   
 [Modos e processamento de armazenamento de partição](../multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)   
 [Armazenamento de dimensões](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)  
  
  
