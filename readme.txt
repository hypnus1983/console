# 获取代码
git clone https://github.com/minio/console.git
cd console

# 首次运行需要安装依赖
go mod tidy

# 编译
make

cd web-app
npm install
npm run build
npm start

# MinIO服务器地址
export CONSOLE_MINIO_SERVER=http://localhost:9000

# Console访问凭证(用于加密JWT)
export CONSOLE_PBKDF_PASSPHRASE=SECRET
export CONSOLE_PBKDF_SALT=SECRET

# 开发模式(可选)
export CONSOLE_DEV_MODE=on

# 使用mc工具创建用户
mc admin user add myminio/ console YOURPASSWORD

# 创建管理策略
mc admin policy create myminio consoleAdmin admin.json

# 绑定策略到用户
mc admin policy attach myminio consoleAdmin --user=console

./console server
