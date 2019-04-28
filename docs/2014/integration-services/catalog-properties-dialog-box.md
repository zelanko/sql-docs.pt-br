---
title: Caixa de diálogo Propriedades do catálogo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.iscatalogprop.general.f1
- sql12.ssis.ssms.iscreatecatalog.f1
ms.assetid: 3e2fcf11-e010-41c6-bc26-e4b281c0bfbc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 849346f33a3118029a46241644d7f1cce6dc7481
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62836245"
---
# <a name="catalog-properties-dialog-box"></a>Caixa de diálogo Propriedades do Catálogo
  Use a caixa de diálogo de Propriedades do Catálogo para configurar o catálogo do SSISDB. As propriedades do catálogo definem como dados confidenciais são criptografados, como dados de operações e de controle de versão de projeto são retidos, e quando o tempo limite de operações de validação expira. O catálogo do SSISDB é um armazenamento e ponto de administração central para projetos, pacotes, parâmetros e ambientes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Você também pode exibir propriedades do catálogo na exibição catalog.catalog_property e definir propriedades por meio do procedimento armazenado catalog.configure_catalog. Para obter mais informações, consulte [catalog.catalog_properties &#40;banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) e [catalog.configure_catalog &#40;banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database).  
  
 Para obter informações sobre como criar o catálogo do SSISDB, consulte [Criar o catálogo do SSIS](catalog/ssis-catalog.md).  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Propriedades do Catálogo](#open_dialog)  
  
-   [Configurar as opções](#options)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Propriedades do Catálogo  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Conecte-se ao Mecanismo de Banco de Dados do Microsoft SQL Server.  
  
3.  No Pesquisador de Objetos, expanda o nó **Integration Services** , clique com o botão direito do mouse em **SSISDB**e clique em **Propriedades**.  
  
##  <a name="options"></a> Configurar as opções  
  
### <a name="options"></a>Opções  
 A tabela a seguir descreve determinadas propriedades na caixa de diálogo e as propriedades correspondentes na exibição de catalog.catalog_property.  
  
|Nome da Propriedade (caixa de diálogo Propriedades do Catálogo)|Nome da Propriedade (exibição catalog.catalog_property)|Descrição|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|Nome do Algoritmo de Criptografia|ENCRYPTION_CLEANUP_ENABLED|Especifica o tipo de criptografia usado para criptografar os valores dos parâmetros confidenciais no catálogo. O valores possíveis são os seguintes:<br /><br /> **DES**<br /><br /> **TRIPLE_DES**<br /><br /> **TRIPLE_DES_3KEY**<br /><br /> **DESPX**<br /><br /> **AES_128**<br /><br /> **AES_192**<br /><br /> **AES_256** (default)|  
|Tempo Limite de Validação (segundos)|VALIDATION_TIMEOUT|Especifique o número máximo de segundos que a validação de um projeto ou de um pacote pode ser executada antes de ser parada. O valor padrão é 300 segundos.<br /><br /> A execução da validação é uma operação assíncrona. Quanto maior for o projeto ou o pacote, mais tempo será necessário para a validação.<br /><br /> Para obter informações sobre como validar projetos e pacotes, consulte [Tipos de dados do Integration Services em expressões](expressions/integration-services-data-types-in-expressions.md).|  
|Limpar Logs Periodicamente|OPERATION_CLEANUP_ENABLED|Defina a propriedade como True para indicar que o trabalho do SQL Server Agent, limpeza de operações, é executada. Caso contrário, defina a propriedade como False.|  
|Período de Retenção (dias)|RETENTION_WINDOW|Especifique a idade máxima dos dados de operações permitidos (em dias). Dados mais antigos do que o número de dias especificado serão removidos pelo trabalho do SQL Agent, limpeza de operações.|  
|Número Máximo de Versões por Projeto|MAX_PROJECT_VERSIONS|Especifique quantas versões de um projeto serão armazenadas no catálogo. Versões de projetos mais antigas que excederem o número máximo serão removidas quando o trabalho de limpeza de versões do projeto for executado.|  
  
  
