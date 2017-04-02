---
title: "Usar o sqlBindR.exe para atualizar uma inst&#226;ncia do R Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server (starting with 2016 CTP3)"
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Usar o sqlBindR.exe para atualizar uma inst&#226;ncia do R Services
O Microsoft R Server para Windows contém uma nova ferramenta, chamada **SqlBindR.exe**, que pode ser usada para atualizar os componentes do R de uma instância. Esse processo é chamado **associação**, pois muda o modelo de licenciamento para que uma instância do SQL Server 2016 use a nova licença do Suporte do Ciclo de Vida de Software Moderno Microsoft.

Em geral, esse sistema de licenciamento garante que seus cientistas de dados sempre usarão a última versão do R. Para obter mais informações sobre os termos e as vantagens da Licença para Software Microsoft, consulte [Run Microsoft R Server for Windows](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev) (Executar o Microsoft R Server para Windows).

Quando você associa uma instância, três coisas acontecem:
+ A política de suporte da instância é alterada da política de suporte do SQL Server 2016 para o novo contrato de Licença para Software Moderno Microsoft.
+ Os componentes do R associados a essa instância serão atualizados automaticamente com cada versão, em sincronia com a versão do R Server atual, de acordo com os novos termos da Licença para Software Moderno.
+ A instância não poderá mais ser atualizada manualmente, exceto para a adição de novos pacotes. 

Se, posteriormente, você decidir que deseja parar de atualizar a instância a cada versão, será necessário **desassociar** a instância e, em seguida, desinstalar os componentes do Microsoft R Server, conforme descrito no artigo [Run Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) (Executar o Microsoft R Server para Windows). Quando o processo for concluído, as atualizações futuras do R Server não afetarão mais a instância.

> [!NOTE] Há suporte para o processo de atualização apenas nas instâncias do SQL Server 2016 corrigidas com a Atualização Cumulativa 3.0.  
> 
> Se você estiver usando o R Services no SQL Server vNext, não será necessário aplicar essa atualização. Os componentes do R são sempre atualizados automaticamente em cada marco.

## <a name="how-to-upgrade-an-instance"></a>Como atualizar uma instância


1. Execute o instalador do Microsoft R Server no computador que tem a instância que você deseja atualizar.
2. Quando a instalação for concluída, localize a pasta que contém a ferramenta **SqlBindR.exe**. A localização padrão é: `C:\Program Files\Microsoft\R Server\Setup`
2. Abra um novo prompt de comando como administrador.
3. Digite o seguinte comando para exibir uma lista das instâncias disponíveis: `SqlBindR.exe /list`
4. Execute o comando **SqlBindR.exe** com o argumento */bind* para especificar o nome da instância a ser atualizada. 
   Por exemplo, para atualizar apenas a instância padrão, digite:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

## <a name="how-to-downgrade-an-instance-of-r-services"></a>Como fazer downgrade de uma instância do R Services

Para reverter o status de uma instância, é necessário executar a ferramenta SqlBindR para remover o licenciamento e, em seguida, reparar ou reinstalar a instância.

1. Execute o comando **SqlBindR.exe** com o argumento */unbind* e especifique a instância. 
   Por exemplo, o seguinte comando reverte a instância padrão para que ela esteja em conformidade com o licenciamento e o agendamento de atualização do SQL Server:  `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`
2. Restaure a instância para o status original seguindo um destes procedimentos:
    + Repare a instância. A operação de reparo aplicará atualizações a todos os recursos instalados.
    + Desinstale e reinstale e, em seguida, aplique todas as liberações de serviço. A instância deve ser reiniciada.
3. Após a remoção do R Server, os pacotes que foram instalados com a instância também serão removidos e, portanto, deverão ser reinstalados.

## <a name="requirements"></a>Requisitos
Há suporte à atualização apenas nas instâncias do SQL Server 2016 que atendem aos seguintes requisitos:
+ SQL Server 2016 SP1 ou posterior
+ A Atualização Cumulativa 3.0 (OD) foi aplicada

No momento, há suporte à atualização apenas com o uso da ferramenta de linha de comando. Uma interface interativa será fornecida em uma versão posterior.

## <a name="sqlbindrexe-command-syntax"></a>sintaxe do comando sqlbindr.exe


### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parâmetros

|Nome|Description|
|------|------|
|*list*| Exibe uma lista de todas as IDs de instância do Banco de Dados SQL no computador atual|
|*bind*| Atualiza a instância do Banco de Dados SQL especificada para a última versão do R Server e garante que a instância obtém automaticamente as atualizações futuras do R Server|
|*unbind*|Desinstala a última versão do R Server da instância do Banco de Dados SQL especificada e impede que atualizações futuras do R Server afetem a instância|

### <a name="errors"></a>Erros

A ferramenta retorna as seguintes mensagens de erro:

|Erro|Resolução|
|------|------|
|Erro ao associar a instância| A instância não pôde ser associada. Contate o suporte para obter assistência.|
|A instância já está associada| Você executou o comando *bind*, mas a instância especificada já está associada. Escolha outra instância.|
|A instância não está associada| Você executou o comando *unbind*, mas a instância especificada não está associada. Escolha outra instância.|
|ID de instância SQL inválida| Você pode ter digitado o nome da instância incorretamente. Execute o comando novamente com o argumento *list* para ver as IDs de instância disponíveis.|
|Nenhuma instância encontrada| Este computador não tem uma instância do SQL Server R Services.|
|A instância deve ter uma versão compatível do SQL R Services (no Banco de Dados) instalada.| Consulte https://go.microsoft.com/fwlink/?linkid=835761 para obter mais detalhes|
|Erro ao desassociar a instância| A instância não pôde ser desassociada. Contate o suporte para obter assistência.|
|Erro inesperado| Outros erros. Contate o suporte para obter assistência.  |
|Nenhuma instância SQL encontrada| Este computador não tem uma instância do SQL Server. |


## <a name="see-also"></a>Consulte também

[Notas de versão do R Server](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)
