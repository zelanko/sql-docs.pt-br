---
title: Use o Assistente de geração de esquema (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Schema Generation Wizard, steps
- relational schema [Analysis Services], Schema Generation Wizard
ms.assetid: 8c710745-d41d-4c31-b6a2-2956229df75a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da833d9c71b93405369a1fee1d7947784d2a09e8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210166"
---
# <a name="use-the-schema-generation-wizard-analysis-services"></a>Use o assistente de geração de esquema (Analysis Services)
  O Assistente de Geração de Esquema requer uma quantidade limitada de informações durante a fase de geração. A maioria das informações que o Assistente de Geração de Esquema requer para gerar esquemas relacionais é extraída dos cubos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e dimensões que você já criou no projeto. Além disso, você pode personalizar como o esquema de banco de dados de área de assunto é gerado e como são nomeados objetos no esquema.  
  
## <a name="start-the-wizard"></a>Inicie o assistente  
 É possível abrir o Assistente de Geração de Esquema a partir do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] de vários modos diferentes:  
  
-   Clique com o botão direito do mouse no objeto do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, clique em **Novo Esquema Relacional** no menu de contexto.  
  
-   Clique no objeto do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, clique em **Novo Esquema Relacional** no menu **Banco de Dados** .  
  
-   Inicie o assistente por meio do Assistente para Dimensões clicando na caixa de seleção **Gerar Esquema Agora** na última página do assistente.  
  
## <a name="step-1-specify-targets"></a>Etapa 1: Especificar destinos  
 Especifique a DSV (exibição da fonte de dados) na qual deseja que o Assistente de Geração de Esquema gere o esquema para o banco de dados da área de assunto. Embora você possa selecionar um DSV existente, normalmente você cria um novo com base em uma fonte de dados. Você pode criar a fonte de dados a partir de uma conexão existente ou nova ou de um outro objeto. O Assistente de Geração de Esquema gera o esquema para o banco de dados da área de assunto no banco de dados de referência da fonte de dados, bem como a exibição da fonte de dados. O Assistente de Geração de Esquema não criará o banco de dados da área de assunto; ele criará o esquema relacional que oferece suporte aos cubos e às dimensões de um banco de dados existente que você especificar.  
  
 Ao gerar os objetos subjacentes, o Assistente de Geração de Esquema associará as dimensões e os cubos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] às tabelas e colunas geradas usando associações no estilo de exibição da fonte de dados.  
  
> [!NOTE]  
>  Para desassociar dimensões e cubos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dos objetos gerados anteriormente, exclua a exibição da fonte de dados à qual as dimensões e os cubos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] foram associados e, em seguida, defina uma nova exibição da fonte de dados para eles usando o Assistente de Geração de Esquema.  
  
## <a name="step-3-specify-schema-options-for-the-subject-area-database"></a>Etapa 3: Especificar opções de esquema para o banco de dados da área de assunto  
 O Assistente de Geração de Esquema oferece inúmeras opções para definição do esquema que é gerado para o banco de dados da área de assunto. Você pode especificar essas opções na página **Opções de Esquema de Banco de Dados da Área de Assunto** do assistente.  
  
### <a name="specifying-the-schema-owner"></a>Especificando o proprietário do esquema  
 Você pode especificar o proprietário do esquema configurando o valor de **Esquema de propriedade** como uma cadeia de caracteres válida. O proprietário padrão do esquema é o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , mas você pode especificar qualquer proprietário de esquema desejado.  
  
### <a name="specifying-primary-keys-indexes-and-constraints"></a>Especificando chaves primárias, índices e restrições  
 Por padrão, o Assistente de Geração de Esquema cria uma restrição de chave primária em cada tabela de dimensões do banco de dados da área de assunto. A chave primária corresponde ao atributo que é designado como o atributo de chave na dimensão correspondente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Essa restrição melhora o desempenho do processamento na maioria dos ambientes, a um custo mínimo. As chaves primárias lógicas são sempre criadas na exibição da fonte de dados, mesmo que você decida não criar a chave primária no banco de dados da área de assunto. Para definir restrições de chave primária em tabelas de dimensões, selecione **Criar chaves primárias em tabelas de dimensões**.  
  
 Por padrão, o assistente também criará índices nas colunas de chave estrangeira em cada tabela de fatos. Eles melhoram o desempenho de processamento na maioria dos ambientes. Normalmente, o desempenho melhora porque as consultas de processamento geradas pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para recuperar novos dados do banco de dados da área de assunto, em geral, contêm um número considerável de instruções de junção entre a tabela de fatos e as tabelas de dimensões. Para definir índices nas colunas de chave estrangeira de cada tabela de fatos, selecione **Criar índices**.  
  
 Finalmente, por padrão, o assistente impõe a integridade referencial entre a tabela de fatos e cada uma das tabelas de dimensões. Se você preferir não impor a integridade referencial, o Assistente de Geração de Esquema ainda criará essas relações no banco de dados e na exibição da fonte de dados. Para impor a integridade referencial, selecione **Impor a integridade referencial**.  
  
### <a name="preserving-data-for-incremental-generation"></a>Preservando dados para geração incremental  
 Por padrão, o Assistente de Geração de Esquema tentará preservar os dados quando o esquema do banco de dados for gerado novamente. Se o Assistente de Geração de Esquema tiver que excluir alguma linha devido a uma alteração no esquema, você receberá um aviso antes dessa exclusão. Por exemplo, talvez seja necessário excluir linhas para resolver problemas de integridade referencial porque você descartou uma dimensão ou porque o tipo de dados mudou quando você alterou um atributo da dimensão. Para preservar os dados quando o esquema de banco de dados for gerado novamente, selecione **Preservar os dados na regeneração**.  
  
## <a name="step-4-specify-naming-conventions"></a>Etapa 4: Especificar convenções de nomenclatura  
 É possível definir as convenções de nomenclatura que o Assistente de Geração de Esquema usará ao gerar determinados objetos no banco de dados da área de assunto na página **Especificar Convenções de Nomenclatura** do assistente. Para obter mais informações sobre as opções disponíveis na página **Especificar Convenções de Nomenclatura**, consulte [Especificar Convenções de Nomenclatura &#40;Assistente de Geração de Esquema&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](../specify-naming-conventions-schema-generation-analysis-services-multidimensional-data.md).  
  
  
