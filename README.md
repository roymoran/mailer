# Mailer 

## Summary
This is a .NET Core background service that listens to a message broker, Azure Service Bus, for the JSON representation of [this message](./Mailer/DTOs/EmailMessage.cs) and sends the message as an email via the SendGrid v3 API endpoint [`/mail/send`](https://sendgrid.com/docs/API_Reference/Web_API_v3/Mail/index.html).


## Quick Start
### Build, Test, Develop
Before running - set the required environment variables found in [AppSettings.cs](./Mailer/AppSettings.cs). More info on settings environment variables for development [here](https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-2.2&tabs=linux). You can safely ignore `EmailConfiguration`.

```bash
git clone git@github.com:roymoran/mailer.git
cd mailer/Mailer

# Install dependencies
dotnet restore

# Run tests
dotnet test

# Develop
dotnet run --project Mailer
```

###  Deploy
```bash
# Build docker image, change namespace/image name as needed
docker build --build-arg SERVICE_BUS_CONNECTION_STRING="provide_your_variable" --build-arg SERVICE_BUS_QUEUE_NAME="provide_your_variable" --build-arg SEND_GRID_API_KEY="provide_your_variable" -t mailer:latest -f ci/Dockerfile .
```

Deploy built docker image to your hosting provider. 

