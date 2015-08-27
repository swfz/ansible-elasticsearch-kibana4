# ansible-elasticsearch-kibana4

* クラスタ構成、ec2までカバー

## 設定
### クラスタ構成か一台構成か分ける

* stage_vars/{stage}.yml
```
elasticsearch:
  composition: [cluster|alone]
```

### 他環境に合わせて変更
* stage_vars/{stage}.yml
* hosts.{stage}

# インストール

* configのみ変更の場合は`--tags "cron|config"`を追加する

```
ansible-playbook -i hosts.{stage} site.yml [--tags "config"]
```

