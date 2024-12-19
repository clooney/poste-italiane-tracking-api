Poste Italiane Tracking API - .Net
================================
Use .Net to track Poste Italiane shipments with Poste Italiane Tracking API.

Features
--------
- Real-time Poste Italiane tracking.
- Batch Poste Italiane tracking.
- Other features to manage your Poste Italiane tracking.

Installation
------------

Downloading the NuGet package using the dotnet CLI

    $ dotnet add package trackingmore
    
Downloading NuGet Packages with the NuGet Command Line Tool

    $ nuget install trackingmore
    
The difference with dotnet cli is that you need to manually modify the .csproj file and add the following code

    <ItemGroup>
        <PackageReference Include="TrackingMore" Version="0.1.1" />
    </ItemGroup>

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your Poste Italiane shipments.

Usage
----------

Create a tracking (Real-time tracking):

      using TrackingMoreAPI;
      using TrackingMoreAPI.Model.Trackings;
    
      namespace Testing;
      
      public class Test
      {
      
            static void Main(string[] args)
            {
              try
              {
                  string apiKey = "your api key";
                  TrackingMore trackingMore = new TrackingMore(apiKey);
      
                  CreateTrackingParams createTrackingParams = new CreateTrackingParams();
                  createTrackingParams.trackingNumber = "LS988368225NL";
                  createTrackingParams.courierCode = "poste-italiane";
                  var apiResponse = trackingMore.Tracking.CreateTracking(createTrackingParams);
                  Console.WriteLine(apiResponse.meta.code);
                  Console.WriteLine(apiResponse.data.trackingNumber);
                  Console.WriteLine(apiResponse.data.courierCode);
              }
              catch (TrackingMoreException ex)
              {
                  Console.WriteLine("Catch custom exceptions：" + ex.Message);
              }
              catch (TimeoutException ex)
              {
                  Console.WriteLine("Timeout Exception: "  + ex.Message);
              }
              catch (Exception ex)
              {
                  Console.WriteLine("Catch other exceptions:" + ex.Message);
              }
      
            }
      
      }


Create trackings (Max. 40 tracking numbers create in one call):

      using TrackingMoreAPI;
      using TrackingMoreAPI.Model.Trackings;

      namespace Testing;
      
      public class Test
      {
      
            static void Main(string[] args)
            {
              try
              {
                  List<CreateTrackingParams> trackingParamsList = new List<CreateTrackingParams>();

                  CreateTrackingParams trackingParams1 = new CreateTrackingParams
                  {
                      trackingNumber = "LY609319257DE",
                      courierCode = "poste-italiane"
                  };
                  
                  trackingParamsList.Add(trackingParams1);
                  
                  CreateTrackingParams trackingParams2 = new CreateTrackingParams
                  {
                      trackingNumber = "CP098116093IT",
                      courierCode = "poste-italiane"
                  };
                  
                  trackingParamsList.Add(trackingParams2);
                  var apiResponse = trackingMore.Tracking.BatchCreateTrackings(trackingParamsList);
                  Console.WriteLine(apiResponse.meta.code);
                  foreach (var item in apiResponse.data.success)
                  {
                      Console.WriteLine("trackingNumber: " + item.trackingNumber);
                      Console.WriteLine("courierCode: " + item.courierCode);
                  
                      Console.WriteLine();
                  }
                  
                  foreach (var item in apiResponse.data.error)
                  {
                      Console.WriteLine("trackingNumber: " + item.trackingNumber);
                      Console.WriteLine("courierCode: " + item.courierCode);
                  
                      Console.WriteLine();
                  }
              }
              catch (TrackingMoreException ex)
              {
                  Console.WriteLine("Catch custom exceptions：" + ex.Message);
              }
              catch (TimeoutException ex)
              {
                  Console.WriteLine("Timeout Exception: "  + ex.Message);
              }
              catch (Exception ex)
              {
                  Console.WriteLine("Catch other exceptions:" + ex.Message);
              }
      
            }
      
      }


Get status of the shipment:

      using TrackingMoreAPI;
      using TrackingMoreAPI.Model.Trackings;

      namespace Testing;
      
      public class Test
      {
      
            static void Main(string[] args)
            {
              try
              {
                  GetTrackingResultsParams getTrackingResultsParams = new GetTrackingResultsParams();

                  # Perform queries based on various conditions
                  # getTrackingResultsParams.trackingNumbers = "LS988368225NL,CP098116093IT";
                  getTrackingResultsParams.courierCode = "poste-italiane";
                  getTrackingResultsParams.createdDateMin = "2023-08-23T06:00:00+00:00";
                  getTrackingResultsParams.createdDateMax = "2023-09-05T07:20:42+00:00";
                  var apiResponse = trackingMore.Tracking.GetTrackingResults(getTrackingResultsParams);
                  Console.WriteLine(apiResponse.meta.code);
                  foreach (var item in apiResponse.data)
                  {
                  Console.WriteLine("trackingNumber: " + item.trackingNumber);
                  Console.WriteLine("courierCode: " + item.courierCode);
                  
                      Console.WriteLine();
                  }
              }
              catch (TrackingMoreException ex)
              {
                  Console.WriteLine("Catch custom exceptions：" + ex.Message);
              }
              catch (TimeoutException ex)
              {
                  Console.WriteLine("Timeout Exception: "  + ex.Message);
              }
              catch (Exception ex)
              {
                  Console.WriteLine("Catch other exceptions:" + ex.Message);
              }
      
            }
      
      }


Update a tracking by ID:

    using TrackingMoreAPI;
      using TrackingMoreAPI.Model.Trackings;
    
      namespace Testing;
      
      public class Test
      {
      
            static void Main(string[] args)
            {
              try
              {
                  UpdateTrackingParams updateTrackingParams = new UpdateTrackingParams();
                  updateTrackingParams.customerName = "New name";
                  updateTrackingParams.note = "New tests order note";
                  string idString = "97a7b322e346b7353d6dbb6fb37aed39";
                  var apiResponse = trackingMore.Tracking.UpdateTrackingByID(idString, updateTrackingParams);
                  Console.WriteLine(apiResponse.meta.code);
                  if(apiResponse.data != null){
                  Console.WriteLine(apiResponse.data.trackingNumber);
                  Console.WriteLine(apiResponse.data.courierCode);
                  Console.WriteLine(apiResponse.data.customerName);
                  Console.WriteLine(apiResponse.data.note);
                  }
              }
              catch (TrackingMoreException ex)
              {
                  Console.WriteLine("Catch custom exceptions：" + ex.Message);
              }
              catch (TimeoutException ex)
              {
                  Console.WriteLine("Timeout Exception: "  + ex.Message);
              }
              catch (Exception ex)
              {
                  Console.WriteLine("Catch other exceptions:" + ex.Message);
              }
      
            }
      
      }