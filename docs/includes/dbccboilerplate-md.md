Procure falhas de hardware. Execute diagnósticos de hardware e corrija os problemas. Examine também os logs do sistema Windows e do aplicativo, além do log de erros do SQL Server, para verificar se o erro ocorreu em decorrência de falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.

Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação em cache seja o problema, contate o fornecedor do hardware.

Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.

Restaure do backup. Se o problema não estiver relacionado ao hardware e um backup limpo conhecido estiver disponível, restaure o banco de dados do backup.

Execute DBCC CHECKDB Se nenhum backup limpo estiver disponível, execute DBCC CHECKDB sem a cláusula REPAIR para determinar a extensão do dano. DBCC CHECKDB recomendará uma cláusula REPAIR para ser usada. Execute DBCC CHECKDB com a cláusula REPAIR apropriada para reparar o dano.

> **não há suporte para a marca de alerta!**
>  **não há suporte para a marca de alerta!**
>  **não há suporte para a marca de alerta!**

Se a execução de DBCC CHECKDB com uma das cláusulas REPAIR não corrigir o problema, contate seu provedor de suporte.

