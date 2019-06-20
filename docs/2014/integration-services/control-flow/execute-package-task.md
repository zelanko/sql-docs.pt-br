---
title: Tarefa Executar Pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.f1
helpviewer_keywords:
- Execution Package task [Integration Services]
- child packages
- parent packages [Integration Services]
ms.assetid: 042d4ec0-0668-401c-bb3a-a25fe2602eac
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 59b623076e86f3bacf5ae8c6e24b48774e33f670
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831905"
---
# <a name="execute-package-task"></a>Tarefa Executar Pacote
  A tarefa Executar Pacote estende os recursos empresariais do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ao permitir que pacotes executem outros pacotes como parte de um fluxo de trabalho.  
  
 Você pode usar a tarefa Executar Pacote para os seguintes propósitos:  
  
-   Decompor fluxo de trabalho de pacote complexo. Essa tarefa permite decompor o fluxo de trabalho em vários pacotes, que são mais fáceis de ler, testar e manter. Por exemplo, se estiver carregando dados em um esquema de estrela, você poderá criar um pacote separado para preencher cada dimensão e a tabela de fatos.  
  
-   Reutilizando partes de pacotes. Outros pacotes podem reutilizar partes de um fluxo de trabalho de pacote. Por exemplo, você pode criar um módulo de extração de dados que pode ser chamado de diferentes pacotes. Cada pacote que chama o módulo de extração pode realizar diferentes anulações de dados, filtragem ou operações de agregação.  
  
-   Agrupando unidades de trabalho. Unidades de trabalho podem ser encapsuladas em pacotes separados e unidas como componentes transacionais ao fluxo de trabalho de um pacote pai. Por exemplo, o pacote pai executa os pacotes acessório e, com base no sucesso ou fracasso dos pacotes acessório, o pacote pai confirma ou reverte a transação.  
  
-   Controlando segurança de pacote. Os autores de pacote exigeem acesso a apenas uma parte de uma solução de pacote múltiplo. Na separação de um pacote em vários, você pode fornecer um nível de segurança maior, porque pode conceder acesso de autor só aos pacotes relevantes.  
  
 Um pacote que executa outros pacotes geralmente é chamado de pacote pai, e os pacotes que um fluxo de trabalho pai executa são chamados de pacotes filho.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui tarefas que executam operações de fluxo de trabalho, como a execução de executáveis e arquivos em lote. Para obter mais informações, consulte [Execute Process Task](execute-process-task.md).  
  
## <a name="running-packages"></a>Executando pacotes  
 A tarefa Executar Pacote pode executar pacotes filho contidos no mesmo projeto que contém o pacote pai. Para selecionar um pacote filho do projeto, defina a propriedade **ReferenceType** como **Referência de Projeto**e defina a propriedade **PackageNameFromProjectReference** .  
  
> [!NOTE]  
>  A opção **ReferenceType** é somente leitura e será definida como **Referência Externa** se o projeto que contém o pacote não tiver sido convertido no modelo de implantação de projeto. Para obter mais informações sobre conversão, consulte [Implantar projetos no Servidor do Integration Services](../deploy-projects-to-integration-services-server.md).  
  
 A tarefa Executar Pacote pode executar pacotes armazenados no banco de dados msdb do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pacotes armazenados no sistema de arquivos. A tarefa usa um gerenciador de conexões OLE DB para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um gerenciador de conexões de Arquivo para acessar o sistema de arquivos. Para obter mais informações, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) e [Flat File Connection Manager](../connection-manager/flat-file-connection-manager.md).  
  
 A tarefa Executar Pacote também pode executar um plano de manutenção do banco de dados que permite a administração de pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] e planos de manutenção de banco de dados na mesma solução [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Um plano de manutenção de banco de dados é semelhante a um pacote do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , mas um plano pode incluir apenas tarefas de manutenção do banco de dados e sempre é armazenado no banco de dados msdb.  
  
 Se você escolher um pacote armazenado no sistema de arquivos, forneça o nome e o local do pacote. O pacote pode residir em qualquer lugar no sistema de arquivos; não tem que estar na mesma pasta que o pacote pai.  
  
 O pacote filho pode ser executado no processo do pacote pai ou em seu próprio processo. A execução do pacote filho em seu próprio processo exige mais memória, mas oferece mais flexibilidade. Por exemplo, se o processo filho falhar, o processo pai poderá continuar sendo executado.  
  
 De modo contrário, às vezes você pode desejar que os pacotes pai e filho falhem em conjunto como uma unidade, ou que não incorra a sobrecarga adicional de outro processo. Por exemplo, se um processo filho falhar e o processamento subsequente no processo pai do pacote depender do sucesso do processo filho, o pacote filho deveria ser executado no processo do pacote pai.  
  
 Por padrão, a propriedade ExecuteOutOfProcess da tarefa executar pacote é definida como `False`, e o pacote filho é executado no mesmo processo que o pacote pai. Se você definir esta propriedade como `True`, o pacote filho será executado em um processo separado. Isto pode reduzir a velocidade do lançamento do pacote filho. Além disso, se você definir a propriedade como `True`, você não poderá depurar o pacote em uma instalação somente ferramentas. Você deve instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obter mais informações, consulte [Instalar o Integration Services](../install-windows/install-integration-services.md)  
  
## <a name="extending-transactions"></a>Estendendo transações  
 A transação que o pacote pai usa pode se estender ao pacote filho; logo, o trabalho que ambos os pacotes executa pode ser confirmado ou revertido. Por exemplo, o banco de dados insere que as execuções do pacote pai podem ser confirmadas ou revertidas, dependendo das inserções do banco de dados executadas pelo pacote filho, e vice-versa. Para obter mais informações, consulte [Inherited Transactions](../inherited-transactions.md).  
  
## <a name="propagating-logging-details"></a>Propagando detalhes de log  
 O pacote filho executado pela tarefa Executar Pacote pode ou não ser configurado para usar log, mas o pacote filho sempre encaminhará os detalhes de log ao pacote pai. Se a tarefa Executar Pacote for configurada para usar log, a tarefa registrará os detalhes de log a partir do pacote filho. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../performance/integration-services-ssis-logging.md).  
  
## <a name="passing-values-to-child-packages"></a>Passando valores a pacotes filho  
 Com frequência um pacote filho usa valores passados para ele por outro pacote que o chama, normalmente, seu pacote pai. Usar valores de um pacote pai é útil nos seguintes cenários:  
  
-   Partes de um fluxo de trabalho maior são atribuídas a pacotes diferentes. Por exemplo, um pacote baixa dados em base noturna, resume os dados, atribui valores de dados resumidos a variáveis e depois passa os valores a outro pacote para processamento adicional dos dados.  
  
-   O pacote pai coordena dinamicamente tarefas em um pacote filho. Por exemplo, o pacote pai determina o número de dias em um mês corrente e atribui o número a uma variável, e o pacote filho executa uma tarefa esse número de vezes.  
  
-   Um pacote filho exige acesso aos dados derivados dinamicamente do pacote pai. Por exemplo, o pacote pai extrai dados de uma tabela e carrega o conjunto de linhas em uma variável, e o pacote filho executa outras operações nos dados.  
  
 Você pode usar os métodos a seguir para transmitir valores a um pacote filho:  
  
-   **Configurações de pacote**  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece um tipo de configuração, a configuração de Variável do Pacote Pai, para transmitir valores de pacotes pai para pacotes filho. A configuração é construída no pacote filho e usa uma variável no pacote pai. A configuração é mapeada para uma variável no pacote filho ou para a propriedade de um objeto no pacote filho. A variável também pode ser usada nos scripts usados pela tarefa Script ou pelo componente Script.  
  
-   **Parâmetros**  
  
     Você pode configurar a tarefa Executar Pacote para mapear variáveis de pacote pai ou parâmetros, ou parâmetros de projeto, para parâmetros de pacote filho. O projeto deve usar o modelo de implantação de projeto e o pacote filho deve ser contido no mesmo projeto que contém o pacote pai. Para obter mais informações, consulte [Execute Package Task Editor](../execute-package-task-editor.md).  
  
    > [!NOTE]  
    >  Se o parâmetro de pacote filho não for confidencial e mapeado para um parâmetro pai confidencial, o pacote filho não será executado.  
    >   
    >  Há suporte para as seguintes condições de mapeamento:  
    >   
    >  -   O parâmetro de pacote confidencial filho é mapeado para um parâmetro confidencial pai  
    > -   O parâmetro de pacote confidencial filho é mapeado para um parâmetro não confidencial pai  
    > -   O parâmetro de pacote não confidencial filho é mapeado para um parâmetro não confidencial pai  
  
 A variável do pacote pai pode ser definida no escopo da tarefa Executar Pacote ou em um contêiner de pai como o pacote. Se diversas variáveis estiverem disponíveis com o mesmo nome, a variável definida no escopo da tarefa Executar Pacote será usada, ou a variável que tenha o escopo mais próximo da tarefa.  
  
 Para obter mais informações, consulte [Usar os valores de variáveis e parâmetros em um pacote filho](../use-the-values-of-variables-and-parameters-in-a-child-package.md).  
  
### <a name="accessing-parent-package-variables"></a>Acessando variáveis de pacote pai  
 Os pacotes filho podem acessar variáveis de pacote pai usando a tarefa de Script. Ao inserir o nome da variável de pacote pai na página **Script** do **Editor da Tarefa de Script**, não inclua **Usuário:** no nome da variável. Caso contrário, o pacote filho não localizará a variável quando você executar o pacote pai. Para obter mais informações sobre como usar a tarefa Script para acessar variáveis de pacote pai, consulte essa entrada de blog [SSIS: Acessando variáveis em um pacote pai](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/).  
  
## <a name="configuring-the-execute-package-task"></a>Configurando a tarefa Executar Pacote  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Execute Package Task Editor](../execute-package-task-editor.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [SSIS: Você deve executar pacotes filho em processo ou fora de processo? ](https://go.microsoft.com/fwlink/?LinkId=220819), em consultingblogs.emc.com.  
  
-   Entrada de blog, [SSIS: Acessando variáveis em um pacote pai](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/), em andyleonard.blog. 
  
  
