# 设计实现一个订票系统

![数据库设计](https://p.ipic.vip/ky3f5d.png)




```java

claas TicketSystem{
	
	Map<City, List<Cinema> cityMap;

	Cinema[] cinemas;

	Movie[] movies;



	 Map<Movie,List<Cinema>> movie2Cineas ;



	Cinema[] getAllCinema(City city){

	}

	Cinema[] getCinemasByMovie(Long movieId){
		movie2Cineas.get();
	}
	
	Movie[] getMovies(){

	}


	void orderSeat(Cineme cinema, Movie movie, Long scheduleId,int[] seatIds){

	}

}



class City{
	String name;

	
}

class Movie{
	//base info	

}


class Cinema{
	City city;
	//影厅
	Room[] room;

	//纬度
	long latitude;
	//经度
	long longtiitude;
	
	//排期
	Schedule[] schedules;

	Movie[] movilesLive;

}

//大厅
class Hall{
	long id;
	int totalSeats;
	long cinemaId;

}

Seat{
	int seatId;
	int row;
	int column;
	
	int type;

	long cinemaId;
	long hallId;
}

ScheduleHall{
	ScheduleSeat[] schedules;

	Map<Long,ScheduleSeat> seatId2Seat;
	
}

//每一个场次的座位表
ScheduleSeat{
	long seatId;
	Long scheduleId;
	Long movieId;

	BigDecimal price;

	boolean ordered;

	ScheduleSeat up;
	ScheduleSeat down;
	ScheduleSeat left;
	ScheduleSeat right;
}


class Schedule{
	Long scheduleId;
	Long movieId;
	long hallId;
	LocalDateTime start;
	LocalDateTime end;

	BigDecimal price;
}




```