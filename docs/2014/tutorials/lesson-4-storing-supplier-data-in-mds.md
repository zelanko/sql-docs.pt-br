---
title: 'Lição 4: Armazenando dados do fornecedor no MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: bacd9eaf-4d12-4f25-aec7-d785dec1b623
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 363b92c975bd80f4d3298a2082b6cedfee9b1263
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048817"
---
# <a name="lesson-4-storing-supplier-data-in-mds"></a>Lição 4: Armazenando dados do fornecedor no MDS
  O Master Data Services (MDS) é a solução do SQL Server para gerenciamento de dados mestre. O gerenciamento de dados mestre (DMD) descreve os esforços de uma organização para descobrir e definir listas não transacionais de dados.  
  
 Os modelos são o nível mais alto da organização no Master Data Services e organizam a estrutura dos dados mestre. A implementação do MDS pode ter um ou vários modelos, em que cada modelo agrupa dados similares. No geral, os dados mestres podem ser categorizados de uma das quatro maneiras: pessoas, local, coisas ou conceitos. Por exemplo, você pode criar um modelo Product para conter dados relativos aos produtos ou um modelo Customer para conter dados relativos aos clientes. Consulte [Modelos (Master Data Services)](http://msdn.microsoft.com/library/ee633746.aspx) para obter mais detalhes.  
  
 Um modelo pode conter uma ou mais entidades. Cada entidade tem atributos (colunas) e membros (linhas). Cada linha contém os dados mestre. Nesta lição, você criará um modelo Suppliers com duas entidades chamadas Supplier e State. A entidade Supplier terá os seguintes atributos: Code, Name, Contact First Name, Contact Last Name, Contact Email Address, Address Line, City, State, Zip e Country. Consulte [Atributos (Master Data Services)](http://msdn.microsoft.com/library/ee633745.aspx) para obter mais detalhes sobre atributos em geral. Os atributos Code e Name correspondem às colunas SupplierID e Supplier Name no arquivo do Excel chamado Cleansed and Matched Suppliers.  
  
 Um atributo baseado em domínio é um atributo com valores que são preenchidos por membros de outra entidade. Os atributos baseados em domínio impedem que os usuários insiram valores de atributos inválidos. Um valor de atributo só pode ser selecionado na lista suspensa preenchida por outra entidade. Neste tutorial, o atributo State da entidade Supplier é um atributo baseado em domínio com valores da entidade State. Você só pode alterar o valor do atributo State da entidade Supplier para um dos valores da entidade State. Consulte [Atributos com Base em Domínio](../master-data-services/domain-based-attributes-master-data-services.md) para obter mais detalhes.  
  
 Uma hierarquia derivada no MDS é resultado da relação de atributo baseado em domínio no modelo. Neste tutorial, você criará uma hierarquia derivada entre as entidades Supplier e State. Depois que você criar a hierarquia derivada, verá uma lista de estados no navegador do Master Data Manager. Ao clicar em um estado na lista, você verá os fornecedores desse estado no painel direito. Posteriormente, você criará uma hierarquia derivada com base nessa relação. Consulte [Hierarquias Derivadas](../master-data-services/derived-hierarchies-master-data-services.md) para obter mais detalhes.  
  
 Você criou uma base de dados de conhecimento no DQS, utilizou-a para limpar e fazer a correspondência dos dados e, por fim, armazenou os resultados no arquivo Cleansed and Matched Supplier Data.xls. Nesta lição, você carregará os dados limpos e correspondentes no MDS. O DQS contém apenas as informações sobre os dados (metadados), enquanto o MDS armazena os próprios dados (conjunto mestre). Por exemplo: o DQS pode ter informações sobre vários fornecedores, mas o MDS mantêm apenas os fornecedores utilizados por uma empresa.  
  
 Nesta lição, você executará as seguintes tarefas:  
  
1.  Crie o modelo **Suppliers** no **MDS** usando o **Aplicativo Web Master Data Manager**.  
  
2.  Abra o arquivo **Cleansed and Matched Supplier Data.xls** no Excel e use o **Suplemento MDS para Excel** a fim de criar uma entidade chamada **Supplier** e carregar os dados no MDS.  
  
3.  Verifique se os dados foram criados no MDS usando o **Master Data Manager**.  
  
4.  Crie uma entidade chamada **State** e atualize o atributo **State** da entidade **Supplier** para ser um atributo baseado em domínio, dependendo da entidade **State** . Faça isso tudo usando o **Suplemento MDS para Excel**.  
  
5.  Verifique se o atributo baseado em domínio foi criado através do **Master Data Manager** e atualize os valores do atributo **Name** da entidade **State** .  
  
6.  Exiba as atualizações feitas usando o **Master Data Manager** no **Excel**.  
  
7.  Carregue os valores da entidade **State** no **Excel** , adicione um valor e verifique a adição usando o **Master Data Manager**.  
  
8.  Crie e use uma hierarquia derivada através da relação de atributo baseado em domínio entre as entidades **Fornecedor** e **State** (o atributo State da entidade Supplier é do tipo entidade State) usando o **Master Data Manager**.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 1: Criando o modelo Fornecedores modelo usando o Master Data Manager](../../2014/tutorials/task-1-creating-suppliers-model-using-master-data-manager.md)  
  
  
