---
title: Implantação de projetos e pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9bd9e036baa91991352d00f97fcf2c8e689bae6c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372148"
---
# <a name="deployment-of-projects-and-packages"></a>Implantação de projetos e pacotes
  O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dá suporte a dois modelos de implantação, o modelo de implantação de projeto e o modelo de implantação de pacote. O modelo de implantação de projeto permite que você implante seus projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para obter mais informações sobre implantação de projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , consulte [Implantar projetos no servidor do Integration Services](../deploy-projects-to-integration-services-server.md).  
  
 Para obter mais informações sobre o modelo de implantação de pacote, consulte [implantação de pacote &#40;SSIS&#41;](legacy-package-deployment-ssis.md).  
  
## <a name="compare-project-deployment-and-package-deployment"></a>Comparar implantação de projeto e implantação de pacote  
 O tipo de modelo de implantação que você escolhe para um projeto determina quais opções de desenvolvimento e administrativas estão disponíveis para aquele projeto. A tabela a seguir mostra as diferenças e as semelhanças entre o uso do modelo de implantação de projeto e o uso do modelo de implantação de pacote.  
  
|Ao usar o modelo de implantação de projeto|Ao usar o modelo de implantação de pacote|  
|---------------------------------------------|---------------------------------------------|  
|Um projeto é a unidade de implantação.|Um pacote é a unidade de implantação.|  
|Parâmetros são usados para atribuir valores a propriedades de pacote.|As configurações são usadas para atribuir valores a propriedades de pacote.|  
|Um projeto, que contém pacotes e parâmetros, é compilado em um arquivo de implantação de projeto (extensão .ispac).|Os pacotes (extensão .dtsx) e as configurações (extensão .dtsConfig) são salvos individualmente no sistema de arquivos.|  
|Um projeto que contém pacotes e parâmetros é implantado no catálogo do SSISDB em uma instância do SQL Server.|Os pacotes e as configurações são copiados no sistema de arquivos em outro computador. Os pacotes também podem ser salvos no banco de dados MSDB ou em uma instância do SQL Server.|  
|A integração CLR é necessária no mecanismo de banco de dados.|A integração CLR não é necessária no mecanismo de banco de dados.|  
|Os valores dos parâmetros específicos ao ambiente são armazenados em variáveis de ambiente.|Os valores de configuração específicos ao ambiente são armazenados nos arquivos de configuração.|  
|Os projetos e pacotes do catálogo podem ser validados no servidor antes da execução. Você pode usar o SQL Server Management Studio, procedimentos armazenados ou código gerenciado para executar a validação.|Os pacotes são validados antes da execução. Você também pode validar um pacote com o código gerenciado dtExec.|  
|Os pacotes são executados com o início de uma execução no mecanismo de banco de dados. Um identificador de projeto, valores de parâmetros explícitos (opcional) e referências ao ambiente (opcional) são atribuídos a uma execução antes de ela ser iniciada.<br /><br /> Também é possível executar pacotes usando `dtExec`.|Os pacotes são executados usando os utilitários de execução `dtExec` e `DTExecUI`. As configurações aplicáveis são identificadas por argumentos de prompt de comando (opcional).|  
|Durante a execução, os eventos produzidos pelo pacote são capturados automaticamente e salvos no catálogo. Você pode consultar esses eventos com exibições Transact-SQL.|Durante a execução, os eventos produzidos por um pacote não são capturados automaticamente. Um provedor de log deve ser adicionado ao pacote para capturar eventos.|  
|Os pacotes são executados em um processo separado do Windows.|Os pacotes são executados em um processo separado do Windows.|  
|O SQL Server Agent é usado para agendar a execução do pacote.|O SQL Server Agent é usado para agendar a execução do pacote.|  
  
## <a name="features-of-project-deployment-model"></a>Recursos do modelo de implantação de projeto  
 A tabela a seguir lista os recursos que estão disponíveis para projetos desenvolvidos apenas para o modelo de implantação de projeto.  
  
|Recurso|Descrição|  
|-------------|-----------------|  
|Parâmetros|Um parâmetro especifica os dados que serão usados por um pacote. Você pode definir o escopo dos parâmetros no nível do pacote ou do projeto com parâmetros de pacote e de projeto, respectivamente. Os parâmetros podem ser usados em expressões ou tarefas. Quando o projeto é implantado no catálogo, você pode atribuir um valor literal para cada parâmetro ou usar o valor padrão que foi atribuído em tempo de design. Em lugar de um valor literal, você também pode fazer referência a uma variável de ambiente. Os valores de variáveis de ambiente são resolvidos na hora da execução do pacote.|  
|Ambientes|Um ambiente é um contêiner de variáveis que podem ser referenciadas por projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Cada projeto pode ter várias referências de ambiente, mas uma única instância de execução de pacote pode fazer referência apenas a variáveis de um único ambiente. Os ambientes permitem organizar os valores que você atribui a um pacote. Por exemplo, você pode ter ambientes denominados "Desenvolvimento", "Teste" e "Produção".|  
|Variáveis de ambiente|Uma variável de ambiente define um valor literal que pode ser atribuído a um parâmetro durante a execução do pacote. Para usar uma variável de ambiente, crie uma referência de ambiente (no projeto que corresponde ao ambiente que tem o parâmetro), atribua um valor de parâmetro ao nome da variável de ambiente e especifique a referência de ambiente correspondente ao configurar uma instância de execução.|  
|Catálogo do SSISDB|Todos os objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são armazenados e gerenciados em uma instância do SQL Server em um banco de dados chamado de catálogo do SSISDB. O catálogo permite usar pastas para organizar seus projetos e ambientes. Cada instância do SQL Server pode ter um catálogo. Cada catálogo pode ter zero ou mais pastas. Cada pasta pode ter zero ou mais projetos e zero ou mais ambientes. Uma pasta do catálogo também pode ser usada como um limite para permissões para objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|Procedimentos armazenados e exibições do catálogo|Um grande número de procedimentos armazenados e exibições pode ser usado para gerenciar objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no catálogo. Por exemplo, você pode especificar valores para parâmetros e variáveis de ambiente, criar e iniciar execuções e monitorar operações do catálogo. É possível até ver exatamente quais valores serão usados por um pacote antes do início da execução.|  
  
## <a name="project-deployment"></a>Implantação de projeto  
 No centro do modelo de implantação do projeto está o arquivo de implantação do projeto (extensão .ispac). O arquivo de implantação do projeto é uma unidade independente de implantação que inclui apenas as informações essenciais sobre os pacotes e parâmetros do projeto. O arquivo de implantação do projeto não captura todas as informações contidas no arquivo do projeto do Integration Services (extensão .dtproj). Por exemplo, arquivos de texto adicionais que você usa para escrever observações não são armazenados no arquivo de implantação do projeto e, portanto, não são implantados no catálogo.  
  
## <a name="required-tasks"></a>Tarefas necessárias  
  
-   [Implantar projetos no servidor do Integration Services](../deploy-projects-to-integration-services-server.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog [Ideias sobre estratégias de expansão para projetos do SSIS](https://go.microsoft.com/fwlink/?LinkId=245739)em mattmasson.com.  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário dtexec](dtexec-utility.md)  
  
  
