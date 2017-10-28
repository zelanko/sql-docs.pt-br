---
title: "Notas de Versão do SQL Server 2012 SP4 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: 0
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 1d637aa3e820f1acd6dc283030d2cdfa1e6ca074
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="sql-server-2012-sp4-release-notes"></a>Notas de versão do SQL Server 2012 SP4
Este tópico resume as melhorias incluídas com o SQL Server 2012 SP4. Os tópicos também descrevem problemas para examinar antes de instalar ou solucionar problemas da instalação do SP4. As Notas de Versão listadas aqui estão disponíveis somente online, e não em mídia de instalação. Este tópico é atualizado periodicamente, conforme os problemas são descobertos. Para obter uma lista detalhada de correções no SP4, consulte [SQL Server 2012 SP4 Release](https://go.microsoft.com/fwlink/?linkid=846937) (Versão do SQL Server 2012 SP4).  

> O Service Pack 4 inclui todas as atualizações cumulativas do SQL Server 2012 SP3.
  
##<a name="download-pages"></a>Páginas de download
O itens a seguir vinculam-se aos pacotes de download primários para o SQL Server 2012 SP3. As páginas de download têm requisitos de sistema e instruções básicas de instalação.
- [Instalação de Patch do SQL Server 2012 SP4](https://go.microsoft.com/fwlink/?linkid=846829)
- [SQL Server 2012 SP4 Express](https://go.microsoft.com/fwlink/?linkid=846905)
- [Microsoft SQL Server 2012 SP4 Feature Pack](https://go.microsoft.com/fwlink/?linkid=846907)

##  <a name="sp4-performance-and-scale-improvements"></a>Melhorias no desempenho e no dimensionamento do SP4

- **Melhoria no procedimento de limpeza do agente de distribuição** – Um banco de dados de distribuição muito grande causou a situação de bloqueio e de deadlock. Um procedimento de limpeza aprimorado tem como objetivo eliminar alguns desses cenários de bloqueio ou de deadlock. 
- **Dimensionamento do Objeto de Memória Dinâmica** – Particione dinamicamente objetos de memória com base em inúmeros nós e núcleos a serem dimensionados no hardware moderno. A meta da promoção dinâmica é evitar possíveis afunilamentos e particionar automaticamente um objeto de memória thread-safe. Objetos de memória não particionados podem ser promovidos dinamicamente para serem particionados por nó. O número de partições é igual ao número de nós NUMA. Objetos de memória particionados por nó podem ser promovidos mais ainda para serem particionado por CPU, em que o número de partições é igual ao número de CPUs.
- **Habilitar > 8TB para o Pool de buffers** – Habilite um espaço de endereço virtual de 128 TB para uso do pool de buffers
- **Limpeza do controle de alterações** – Melhoria do desempenho e da eficiência da limpeza de controle de alterações para tabelas laterais do Controle de Alterações. 

## <a name="sp4-supportability-and-diagnostics-improvements"></a>Melhorias de diagnóstico e da capacidade de suporte do SP4

- **Suporte de despejos completos para Agentes de Replicação** – Atualmente, se os agentes de replicação encontram uma exceção sem tratamento, o comportamento padrão é criar um minidespejo dos sintomas da exceção. O comportamento padrão requer uma etapa de solução de problemas complexos para exceções sem tratamento. O SP4 introduz uma nova chave do Registro, que é compatível com a criação de um despejo completo para os Agentes de replicação.
- **Aprimoramento do diagnóstico no XML do plano de execução** – O XML do plano de execução foi aprimorado para expor informações sobre sinalizadores de rastreamento, frações de memória para junção de loop aninhada, tempo da CPU e tempo decorrido habilitados. 
- **Melhoria na correlação entre DMVs e XE de diagnóstico** – Os campos Query_hash e query_plan_hash são usados para identificar uma consulta com exclusividade. O DMV define-os como varbinary(8), enquanto XEvent define-os como UINT64. Como o SQL Server não tem “bigint sem sinal”, a conversão nem sempre funciona. Essa melhoria introduz novas colunas de filtro/ação XEvent equivalentes a query_hash e a query_plan_hash, exceto que elas estão definidas como INT64, o que podem ajudar a correlacionar consultas entre XE e DMVs. 
- **Melhor diagnóstico de uso/concessão de memória** – Novo XEvent query_memory_grant_usage (backport do Server 2016 SP1)
- **Adicionar o rastreamento de protocolo a etapas de negociação SSL** – Adicione informações de rastreamento de bit para negociação com êxito/falha, incluindo o protocolo etc. Pode ser útil ao solucionar problemas de cenários de conectividade ao mesmo tempo, por exemplo, que a implantação do TLS 1.2
- **Configuração do nível de compatibilidade correto para o banco de dados de distribuição** – Após a instalação do Service Pack, o nível de compatibilidade do banco de dados de distribuição é alterado para 90. A alteração do nível ocorreu devido a um problema no procedimento armazenado de sp_vupgrade_replication. Agora o SP foi alterado para definir o nível de compatibilidade correto para o banco de dados de distribuição. 
- **Novo comando DBCC para clonar um banco de dados** – O banco de dados clonado é um novo comando DBCC adicionado que permite que usuários avançados, como CSS, solucionem problemas em bancos de dados de produção existentes por meio da clonagem do esquema e dos metadados, sem os dados. A chamada é realizada com clonedatabase DBCC (‘source_database_name’, ‘clone_database_name’). Os bancos de dados clonados não devem ser usados em ambientes de produção. Para ver se um banco de dados foi gerado de uma chamada para o banco de dados clonado, é possível usar o seguinte comando, selecione DATABASEPROPERTYEX('clonedb', 'isClone'). O valor retornado de 1 é true e 0 é false. 
- **Arquivo TempDB e informações de tamanho do arquivo no Log de erros do SQL** – Se o tamanho e o crescimento automático forem diferentes para os arquivos de dados TempDB durante a inicialização, imprima o número de arquivos e dispare um aviso.
- **Mensagens de suporte da IFI no Log de erros do SQL Server** – No log de erros, indique que a Inicialização Instantânea de Arquivo está habilitada/desabilitada
- **Novo DMF para substituir o DBCC INPUTBUFFER** – Uma nova Função de gerenciamento dinâmico sys.dm_input_buffer que usa o session_id como parâmetro é introduzida para substituir DBCC INPUTBUFFER
- **Aprimoramento de XEvents para falha na leitura de roteamento para um Grupo de disponibilidade** – No momento, o XEvent read_only_rout_fail só será acionado se houver uma lista de roteamento presente, mas nenhum dos servidores na lista de roteamento estará disponível para conexões. Essa melhoria inclui informações adicionais para ajudar a solucionar problemas e também é expandida nos pontos de código em que o XEvent é acionado. 
- **Melhoria no tratamento do Service Broker com o failover do grupo de disponibilidade** – No momento, quando o Service Broker é habilitado em Banco de dados do gruo de disponibilidade, durante um failover do grupo de disponibilidade, todas as conexões do Service Broker originadas na Réplica Primária são deixadas abertas. A melhoria fecha todas essas conexões abertas durante um failover do grupo de disponibilidade.
- **[Particionamento do soft-NUMA automático](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx)** – Com o SQL 2014 SP2, O soft-NUMA automático é introduzido quando o Sinalizador de rastreamento 8079 é habilitado no nível do servidor. Quando o Sinalizador de rastreamento 8079 é habilitado durante a inicialização, o SQL Server 2014 SP2 interroga o layout de hardware e configura automaticamente o soft-NUMA em sistemas que reportam oito ou mais CPUs por nó NUMA. O comportamento do soft-NUMa automático tem reconhecimento de hyperthread (HT/processador lógico). O particionamento e a criação de nós adicionais dimensiona o processamento em segundo plano aumentando o número de ouvintes, o dimensionamento e os recursos de rede e de criptografia. É recomendável testar primeiro o desempenho da carga de trabalho com o soft-NUMA automático antes que ele seja ATIVADO na produção.

## <a name="see-also"></a>Consulte também
- [Instalar as atualizações de manutenção do SQL Server 2012](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [Como identificar sua versão de SQL Server e edição](https://support.microsoft.com/en-us/help/321185)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

