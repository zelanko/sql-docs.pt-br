---
title: Suplemento Master Data Services para Microsoft Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f58a349ebf67f710b4ff4722b85328992b3555eb
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371118"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Suplemento do Master Data Services para Microsoft Excel
  Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], listas mestres dos dados de referência podem ser distribuídas para qualquer pessoa da sua organização que usa o Excel. A segurança determina quais usuários dos dados podem ver e atualizar.  
  
 Você pode carregar listas filtradas de dados do MDS no Excel, onde você pode trabalhar com elas da mesma maneira que você trabalharia com outros dados. Quando você terminar, poderá publicar os dados no MDS novamente, onde serão armazenados centralmente.  
  
 Se você for um administrador, também poderá usar o [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] para novas entidades e atributos, e carregá-los com os dados. Isso elimina a necessidade de usar outras ferramentas para carregar dados em seus modelos.  
  
 No [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], você pode usar o DQS (Data Quality Services) para combinar os dados antes de carregá-los no MDS. Isso ajuda a evitar dados duplicados no MDS.  
  
> [!IMPORTANT]  
>  Você pode continuar a usar a versão do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 do suplemento Master Data Services para Excel depois de atualizar o Master Data Services e o Data Quality Services para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. No entanto, qualquer versão anterior do suplemento Master Data Services para Excel não funcionará depois de atualizar para o SQL Server 2014 CTP2. Você pode baixar a versão do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 do suplemento Master Data Services para Excel [aqui](https://go.microsoft.com/fwlink/?LinkId=328664).  
  
## <a name="terms"></a>Termos  
 No suplemento, você poderá encontrar os termos a seguir.  
  
-   O *MDS repository* é onde são armazenados todos os dados mestre. É um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é configurado para armazenar dados do MDS. Para trabalhar com os dados do repositório, você carrega os dados no Excel, ao terminar o trabalho, você publica as alterações no repositório novamente. Os administradores podem adicionar novas entidades e atributos ao repositório.  
  
-   *Dados gerenciados no MDS* são dados armazenados no repositório do MDS e que são carregados no Excel, em que os dados são exibidos como linhas realçadas. Você pode adicionar dados que não sejam gerenciados no MDS à sua planilha, e eles não serão afetados quando você atualizar os dados gerenciados no MDS.  
  
-   Um *model* é um contêiner de dados. As versões desses contêineres podem ser criadas, e normalmente a última versão é o mais recente. Para obter mais informações, consulte [Modelos &#40;Master Data Services&#41;](../models-master-data-services.md).  
  
-   Uma *entity* é uma lista de dados. Você pode pensar em uma entidade como uma tabela em um banco de dados. Por exemplo, a entidade **Cor** pode conter uma lista de cores. Para obter mais informações, consulte [Entidades &#40;Master Data Services&#41;](../entities-master-data-services.md).  
  
-   Um *member* é uma linha de dados. Cada entidade contém membros. Um exemplo de membro é **Azul**. Para obter mais informações, consulte [Membros &#40;Master Data Services&#41;](../members-master-data-services.md).  
  
-   Um *attribute* é uma coluna de dados. Cada membro possui atributos. Por exemplo, o atributo **Código** do membro **Azul** é **B**. Para obter mais informações sobre atributos, consulte [Atributos &#40;Master Data Services&#41;](../attributes-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Crie uma conexão com um repositório do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Carregue os dados gerenciados no MDS no Excel.|[Carregar dados do MDS no Excel](export-data-to-excel-from-master-data-services.md)|  
|Salve um arquivo de consulta de atalho que você possa usar para abrir os dados gerenciados no MDS exibidos atualmente no futuro.|[Salvar um arquivo de consulta de atalho &#40;Suplemento MDS para Excel&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Compartilhe atalhos com outros usuários.|[Enviar um arquivo de consulta de atalho por email &#40;Suplemento MDS para Excel&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Veja todas as alterações que foram feitas em um membro.|[Exibir todas as anotações ou transações de um membro &#40;Suplemento MDS para Excel&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Antes de publicar novos dados, descubra se há duplicação.|[Corresponder dados semelhantes &#40;Suplemento MDS para Excel&#41;](match-similar-data-mds-add-in-for-excel.md)|  
|Publique dados de uma planilha no repositório do MDS.|[Publicar dados do Excel no MDS &#40;suplemento do MDS para Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Crie uma nova entidade com dados na planilha. (Somente para administradores)|[Criar uma entidade &#40;Suplemento MDS para Excel&#41;](create-an-entity-mds-add-in-for-excel.md)|  
|Crie um atributo baseado em domínio, também conhecido como lista restrita. (Somente para administradores)|[Criar um atributo baseado em domínio &#40;Suplemento MDS para Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Defina as propriedades para carregar e publicar dados no Suplemento do Master Data Services para Excel. (Somente para administradores)|[Definir propriedades para o suplemento do Master Data Services para Excel](setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Conexões &#40;Suplemento MDS para Excel&#41;](connections-mds-add-in-for-excel.md)  
  
-   [Carregamento de dados &#40;suplemento do MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Arquivos de consulta de atalho &#40;Suplemento MDS para Excel&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Correspondência de qualidade de dados no Suplemento do MDS para Excel](data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [Publicação de dados &#40;suplemento do MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Criando um modelo &#40;Suplemento MDS para Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
-   [Segurança &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  
